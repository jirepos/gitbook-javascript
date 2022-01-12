# TypeScript (1) - Installation 



TypeScript는 JavaScript와 특이한 관계에 있습니다. TypeScript는 JavaScript의 모든 기능과 그 위에 추가 계층인 TypeScript의 유형 시스템을 제공합니다.

https://www.typescripttutorial.net/



## 설치
전역으로 설치 
```shell
npm install -g typescript
```

버전확인
```shell
tsc --v
```

## helloworld
helloworld 폴더를 생성하고 helloworld.ts 생성한다. 
```typescript
let message: string = 'Hello, World!';
console.log(message);
```
terminal에서 다음을 입력
```shell
tsc hello.ts
```
그럼 hello.js가 생성된다. 
```shell
hello.js
hello.ts
```
