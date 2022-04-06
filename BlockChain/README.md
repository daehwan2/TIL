## Blockchain

- 블록체인은 암호학과 수학 덕분에 가능한, **영구적 정보의 보관 기술**을 뜻함.
- 새로운 플랫폼 (개발자가 사용할 수있는 플랫폼)
- chain of block 블록들이 모여있는 체인.
- BlockChain 을 **추가만 가능한 데이터베이스라고 생각. ( 편집 , 삭제 불가 )**
- 탈중앙화 : 특정 개인이 DB를 관리할 수 없다는 의미 (모두가 DB의 복재본을 가지고 있음)<br/>
🎉 즉 **분산된 DB**라고 할 수 있다. ( => 감시하거나 통제가 절대적으로 힘듬 )

## 블록이 정보를 DB에 추가하는 방법.
- 블록형태로 정보가 추가됨.
- 데이터 + 해시(수학함수, 일방향 함수, 결정론적)
‼해시 : 수학함수, 일방향 함수(ouput을 가지고 input을 얻을 수 없음) , 결정론적( input 에대한 output이 정해져있음. )

=> 결국 필요한 것: ( 데이터 + 이전 블록의 해시 ) 해시


typescript로 만든 blockchain

검증과정을 최소화시킨버젼

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
