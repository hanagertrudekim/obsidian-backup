---
tags:
  - electron
  - SNU
---
## Electron이란? 
- javascript, html, css사용한 **데스크탑앱 개발 프레임워크**
- **node js + chromium**
	- 백엔드와 프론트엔드 영역이 공존
	- node.js
		- 백엔드의 영역
		- node.js 기반으로 사용할수있는 모든 모듈들을 사용 가능
	- chromium
		- 프론트엔드의 영역
		- 크롬 확장 배포판
		- 웹의 브라우저가 있듯이, electron에는 chromium 브라우저를 사용하여 화면을 구성
- **크로스 플랫폼 지원**
	- window, mac, linux 프로그램 작업 및 배포 가능
- **동작 방식**
	- ipc process 기반으로 동작
		- 서버와 브라우저 간 통신을 하기 위한 규약
		- **main process**
		- **renderer process**
			- frontend process
			- 서로 독립적으로 동작

## IPC precess
- electron에서 사용되는 기술
	- 웹기술에 빗대자면, 프론트와 백엔드간의 통신을 위해서 필요한 모듈?
- **프로세스 간 통신**
	- **Main-process** 와 **Renderer-process** 간에 동기적, 비동기적으로 통신함
		- main-process => **node.js (backend)**
		- renderer-process => **chromium (frontend)**
	- 직력화 된 json메시지로 주고받음 
- 브라우저와 서버간의 데이터를 주고받아야하기 때문에, main으로 form 데이터를 보내고, main에서 파이썬 스크립트를 호출하면서 데이터를 전달하는 식으로 생각함


### Main Processor
- backend process
	- `main.js` 파일로 구축
	- 앱은 단 하나의 main process를 가짐
- node.js 기반
	- node.js 기반의 모듈들 사용 가능
- **electron 시스템에 동작하는 애플리케이션을 제어하는 프로세스**
	- renderer process를 관리
- 대표 프로세스
	- ipcMain

### Renderer Processor
- frontend process
	- 여러개 존재 가능 ,  main process와 1: n 관계
- chromium 기반
	- 브라우저 창을 관리하는 모듈
- 대표 프로세스
	- ipcProcessor
		- main 프로세스로 동기, 비동기 메시지를 보낼수있음

### message, event 전달
``` js 
- ipc에서 on을 통한 이벤트 수신(받기)
ipcMain.on('CHANNEL_NAME', (evt, payload) => { })
```
```js
- ipc에서 send를 통한 이벤트 송신(보내기)
ipcRenderer.send('CHANNEL_NAME', 'message')
```

### 파일 구조
- boiler palate에서 제공하는 파일 구조를 살펴보면 대표적으로 두개로 나뉘어진다.
  사람마다 정의하는것은 다르겠지만, 나는 이렇게 구분하기로했다.
	- main (backend, server)
		- main-ipc가 통신하는곳
		- preload.ts (rendere 정의함)
	- renderer (frontend, browser)
		-  renderer-ipc가 통신하는곳


## module
### dialog

> Display native system dialogs for opening and saving files, alerting, etc.

- **파일을 열거나 저장할수있는 모듈**
- 알림을 표시하기 위한 네이티브 시스템 대화 상자를 표시
- 파일이나 디렉터리를 다중으로 선택하는 예시 코드
	- 렌더러 프로세스에서 열고싶다면, `remote` 를 통해 접근
```js 
const { dialog } = require('electron')
console.log(dialog.showOpenDialog(
	{ properties: ['openFile', 'multiSelections'] }))
```
#### method
- dialog 모듈은 다음과 같은 메서드를 가지고있다.
```js
dialog.showOpenDialogSync([browserWindow, ]options)
```
- browerWindow(opt)
	- allows making it modal in parent window
- options : object
	- buttonLabel : custom label for the confirm btn
	- filters : filefilter[]
	- properites : features the dialog should use
		- openFile : allow file select
		- openDirectory : allow directories select
			- window 와 linux 에서는 don't allow both a file, directory selector 