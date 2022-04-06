https://nomadcoders.co/typescript-for-beginners/lectures

## 노마드 코더님의 typescript 강의를 듣고 정리한 문서입니다.

### TypeScript 란?
- superset of javascript
- 자바스크립트의 superset
- 자바스크립트처럼 생긴 프로그래밍 언어
- 컴파일 하면 자바스크립트로 컴파일
- javascript의 업그레이드버젼 느낌..

### TypeScript 사용이유
- javascript가 엄격한 규칙이 없어서 사용하기 편하지만 큰 프로젝트를 하게될때 이러한 점은 치명적인 단점이 됨.

### 초기 세팅 기본 설정
- `npm i -g typescript` 로 설치
- tsconfig.json 파일 생성해서 옵션 설정  => **`tsc -init` 으로 만드는게 편한것같다.**

```json
{
  "compilerOption": {
    "module": "commnjs",
    "target": "ES2015",
    "sourceMap": true
  },
  "include": ["index.ts"],
  "exclude": ["node_modules"]
}

```

- .ts 파일 만들고 ( ex. index.ts)
- 커맨드창에 `tsc` 명령어 입력. ( **typescript를 javascript로 컴파일하는 명령어** )
- 편의를 위해 package.json 에 스크립트 추가.
```json
{
  "name": "typescript-for-beginner",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "prestart": "tsc"
  },
  "author": "",
  "license": "ISC"
}

```

- 컴파일 후 바로 실행 할 수 있도록....


### 추후에 typescript 코드를 수정할때마다 npm run start를 해주어야하는 번거로움이 있다.
> 이를 해결하기위해 tsc-watch 를 설치하고 package.json을 수정해서 start script를 변경해준다.
```json
{
  "name": "typescript-for-beginner",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "tsc-watch --onSuccess \" node dist/index.js\" "
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "tsc-watch": "^5.0.2"
  },
  "devDependencies": {
    "typescript": "^4.6.3"
  }
}

```

> 이 때 tsconfig.json ( **tsc -init 기본세팅으로 하고 outDir만 변경해주었다.**
```json
{
  "compilerOptions": {
    "target": "es2016",
    "module": "commonjs",
    "outDir": "./dist",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,

    "strict": true,
    "skipLibCheck": true
  }
}

```

**이렇게 하면 코드가 변경될때마다 dist폴더하위에 컴파일된 파일이 생기며 컴파일이 끝났을 때 node 명령어가 호출되어서 실행된다**
### TypeScript의 장점
- 매개변수의 자료형 지정 가능
```typescript
const name = "Daehwan2",
  age = 33,
  gender = "male";

const sayHi = (name: string, age: number, gender: string): string => {
  return `Hello ${name}, ${age}, ${gender}`;
};

console.log(sayHi(name, age, gender));

export {};

```
- interface 제공 ( 컴파일시 js로 컴파일되지않음.)
```typescript
interface Human {
  name: string;
  age: number;
  gender: string;
}
const person = {
  name: "daehwan2",
  age: 24,
  gender: "male",
};

const sayHi = (person: Human): string => {
  return `Hello ${person.name}, ${person.age}, ${person.gender}`;
};

console.log(sayHi(person));

export {};

```

- class 의 내부를 선언하고 사용해야 함. 접근지정자도 가능. static 함수도 가능
```typescript
class Human {
  public name: string;
  public age: number;
  public gender: string;
  constructor(name: string, age: number, gender: string) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
}

const human = new Human("daehwan2", 24, "male");
const sayHi = (human: Human): string => {
  return `Hello ${human.name}, ${human.age}, ${human.gender}`;
};

console.log(sayHi(human));

export {};

```
---
#### 전체적으로 내가 봤을때의 장점
- 전체적으로 봤을 때 c나 c++ 등 다른 언어와 같이 자료형을 제공한다.
- 매개변수에 타입을 지정할 수 있고 문법이 엄격해졌다.
- 자바스크립트에서 기본적으로 제공되는 오버로딩기능이 엄격해졌다.
##### **자바스크립트도 객체지향언어지만 문법적으로 너무 자유로워서 가독성측면이나 디테일부분에서 부족했다고 생각하는데 typescript가 이부분을 채워 준 것 같다.**



# 전체적인 사용 예시 (문법적으로 보자) BlockChain 만들기
---
[BlockChain](https://github.com/daehwan2/TIL/issues/4)에 대해 간단하게 이해하고 코드를 보면 이해할 수 있다.
https://github.com/daehwan2/TIL/issues/4
### typescript로 만든 blockchain

```typescript
import * as CryptoJS from "crypto-js";

class Block {
  static calculateBlockHash = (
    index: number,
    previousHash: string,
    timestamp: number,
    data: string
  ): string =>
    CryptoJS.SHA256(index + previousHash + timestamp + data).toString();

  static validateStructure = (aBlock: Block): boolean =>
    typeof aBlock.index === "number" &&
    typeof aBlock.hash === "string" &&
    typeof aBlock.previousHash === "string" &&
    typeof aBlock.timestamp === "number" &&
    typeof aBlock.data === "string";

  public index: number;
  public hash: string;
  public previousHash: string;
  public data: string;
  public timestamp: number;

  constructor(
    index: number,
    hash: string,
    previousHash: string,
    data: string,
    timestamp: number
  ) {
    this.index = index;
    this.hash = hash;
    this.previousHash = previousHash;
    this.data = data;
    this.timestamp = timestamp;
  }
}

const genesisBlock: Block = new Block(
  0,
  "202031210312313",
  "",
  "hello",
  123456
);

let blockChain: [Block] = [genesisBlock]; //Block 객체만 받을수있는 배열

const getBlockchain = (): Block[] => blockChain;

const getLatestBlock = (): Block => getBlockchain()[blockChain.length - 1];

const getNewTimeStamp = (): number => Math.round(new Date().getTime() / 1000);

const createNewBlock = (data: string): Block => {
  const previousBlock: Block = getLatestBlock();
  const newIndex: number = previousBlock.index + 1;
  const newTimestamp: number = getNewTimeStamp();
  const newHash: string = Block.calculateBlockHash(
    newIndex,
    previousBlock.hash,
    newTimestamp,
    data
  );

  const newBlock: Block = new Block(
    newIndex,
    newHash,
    previousBlock.hash,
    data,
    newTimestamp
  );

  addBlock(newBlock);
  return newBlock;
};

const getHashforBlock = (aBlock: Block): string =>
  Block.calculateBlockHash(
    aBlock.index,
    aBlock.previousHash,
    aBlock.timestamp,
    aBlock.data
  );

const isBlockValid = (candidateBlock: Block, previousBlock: Block): boolean => {
  if (!Block.validateStructure(candidateBlock)) {
    return false;
  } else if (previousBlock.index + 1 !== candidateBlock.index) {
    return false;
  } else if (previousBlock.hash !== candidateBlock.previousHash) {
    return false;
  } else if (getHashforBlock(candidateBlock) !== candidateBlock.hash) {
    return false;
  } else {
    return true;
  }
};

const addBlock = (candidateBlock: Block): void => {
  if (isBlockValid(candidateBlock, getLatestBlock())) {
    blockChain.push(candidateBlock);
  }
};

createNewBlock("second block");
createNewBlock("third block");
createNewBlock("fourth block");

console.log(blockChain);
export {};

```
