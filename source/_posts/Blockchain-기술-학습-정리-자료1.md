---
title: Blockchain 기술 학습 정리 자료1
date: 2022-02-12 13:11:18
tags:
  - Blockchain
categories:
  - Blockchain
---

## 블록체인이란?

- 블록체인은 일반적으로 중앙의 기관 없이 구현되는 분산 방식의 변조 방지 디지털 원장이다. 기본적으로 사용자가 블록체인 네트워크에 트랜잭션을 기록할 수 있으며, 이는 네트워크의 정상적인 작동 하에서 트랜잭션이 게시되면 이는 변경할 수 없다.
- 블록체인은 블록으로 그룹화되어 암호화, 서명화 된 트랜잭션의 분산 디지털 원장이다. 각 블록은 유효성 검사, 합의에 따라 이전 블록과 암호화된 방식으로 연결되며, 새로운 블록은 네트워크 내의 원장 사본에 복사되고, 충돌이 발생한다면 미리 설정한 규칙에 따라 자동적으로 문제를 해결한다.

## 블록체인의 분류 (Permissionless VS Permissioned)

### Permissionless

- 어떠한 기관의 허가 없이 블록을 게시하는 모든 사람에게 개방된 탈중앙화 원장 플랫폼이다.
- 대부분이 오픈 소스 소프트웨어이며, 다운로드하려는 모든 사람이 무료로 사용할 수 있다. 누구나 블록을 게시할 수 있는 권리가 있으므로 일부 악의적인 사용자는 시스템을 전복시키기 위한 목적으로 블록을 게시하려고 시도할 수 있다. 이를 방지하기 위해 합의 시스템(예를 들어, Pos, Pow 등)을 활용한다.
- 합의 시스템은 일반적으로 프로토콜을 준수하는 블록 게시자(Miner, 채굴자)에게 암호화폐를 보상하여 악의적이지 않는 행동을 하도록 한다.

### Permissioned

- 사용자, 또는 노드가 일부 권한을 승인 받아야 하는 블록체인 네트워크이다. (권한의 승인을 중앙 집중형에서 받든, 분산형에서 받든)
- 승인된 개인만이 트랜잭션을 제출할 수 있다. 따라서 무허가 블록체인 네트워크와 같은 리소스를 과하게 소비하는 합의 방식은 필요로 하지 않는다. (이미 승인되어 신뢰할 수 있는 사용자로 보기 때문에)
- 참여하기 위해 본인의 신원 확인이 필요하며, 사로간의 신뢰로 네트워크가 유지된다.

## 블록체인의 구성 요소

### 암호화를 위한 해시 함수

- 블록체인 네트워크에서 해시 함수(SHA-256 등)는 다양한 작업에 사용된다.

#### 사용 예시

- Address derivation.
- Creating unique identifiers.
- Securing the block data: a publishing node will hash the block data, creating a digest that will be stored within the block header.
- Securing the block header: a publishing node will hash the block header. If the blockchain network utilizes a proof of work consensus model, the publishing node will need to hash the block header with different nonce values until the puzzle requirements have been fulfilled. The current block header’s hash digest will be included within the next block’s header, where it will secure the current block header data.

### 암호화 nonce

- nonce는 한번만 사용되는 임의의 숫자이다.
- 데이터와 결합하여 nonce마다 다른 해시를 생성한다.

```
hash(data + nonce) = digest
```

- 즉, nonce 값만 변경하면 동일한 데이터에 대해 다른 다이제스트(digest) 값을 얻을 수 있으며, 이는 작업 증명 합의 모델에서 사용한다.

### 거래

- 블록체인 네트워크의 각 블록에는 0개 이상의 트랜잭션이 포함될 수 있다. 블록체인 네트워크의 보안을 유지하기 위해 새로운 블록의 지속적인 공급은 매우 중요하다. 이를 위해 트랜잭션이 발생하지 않더라도 지속해서 블록을 생성하여야 한다.
- 새로운 블록을 지속적으로 공급함으로써 악의적인 사용자가 더 길고 위조된 블록체인을 제조하는 것을 방지한다.
- 또한, 거래의 유효성과 신뢰성을 결정하는 것은 매우 중요하다. 트랜잭션의 유효성은 프로토콜 요구 사항 및 블록체인 네트워크의 구현과 관련된 모든 형식화된 데이터 형식, 또는 스마트 계약 요구 사항을 충족하는 지 확인한다. 거래의 진위 여부는 디지털 자산의 발신자가 해당 디지털 자산에 엑세스할 수 있는지 여부를 결정하므로, 매우 중요하다.
- 트랜잭션은 일반적으로 발신자의 개인 키로 디지털 서명되며, 매칭되는 공개 키를 이용하여 언제든지 확인할 수 있다.

<p align="center"><img src="/images/Blockchain/BasicStudy/BlockchainBasic1.JPG"></p>

### 비대칭키 암호화 (공개키 암호화)

- 블록체인 네트워크의 사용자가 보유한 개인키로 암호화하고 공개키로 복호화하는 방식을 취할 수 있으며, 반대로 공개키로 암호화하고 개인키로 복호화하는 방식을 취할 수도 있다.
- 키 암호화는 트랜잭션을 공개 상태로 유지하는 동시에 트랜잭션의 무결성과 신뢰성을 확인하는 매커니즘을 제공하여 서로를 모르거나 신뢰하지 않는 사용자 간의 신뢰 관계를 가능하도록 한다.

#### 디지털 서명

- 개인키를 사용하여 트랜잭션을 암호화하면 공개키를 가진 사람들은 누구나 암호를 해독할 수 있다. 공개키는 자유롭게 사용할 수 있으므로, 개인키로 트랜잭션을 암호화하면, 트랜잭션 디지털 서명자가 개인키에 엑세스할 수 있음이 증명된다.
- 또는, 개인키에 액세스할 수 있는 사용자만 암호를 해독할 수 있도록 공개키로 데이터를 암호화할 수도 있다.

##### 디지털 서명 사용 예시

- 블록체인 네트워크에서 사용한다.
- 개인키는 거래를 디지털 서명하는 데에 사용한다.
- 공개키는 주소를 파생하는 데에 사용한다.
- 공개키는 개인키로 생성된 서명을 확인하는 데에 사용한다.
- 비대칭 키 암호화는 다른 사용자에게 화폐 등을 이전하는 사용자가 트랜잭션에 서명할 수 있는 개인키를 소유하고 있음을 증명 및 확인하는 기능을 제공한다.

### 주소 및 주소 파생

- 대부분의 블록체인 구현은 트랜잭션에서 "to" 및 "from"의 엔드포인트를 주소로 사용한다. 주소는 공개키보다 짧으며, 비밀이 아니다. 주소를 생성하는 한가지 방법은 공개키를 만들어 해시를 적용하고, 해시를 텍스트로 변환하는 방법이다.

```
public key -> cryptographic hash function -> address
```

- 주소는 사용자가 블록체인 네트워크에서 공개 식별자 역할을 할 수 있으며, 종종 주소는 모바일에서도 쉽게 사용할수 있도록 QR코드로 변환된다.

### 개인키 저장

- 블록체인 네트워크의 사용자는 자신의 개인키를 관리하고 안전하게 저장해야 한다.
- 사용자가 개인키를 분실한다면 동일한 개인키를 재생성하는 것은 불가능하기 때문에 해당 키와 관련된 모든 디지털 자산이 손실된다. 반대로 개인키를 도난당한다면 공격자는 해당 개인키가 제어하는 모든 디지털 자산에 대해 전체 액세스 권한을 갖는다.
- 암호화폐가 도난 당했다는 것은 일부 개인키가 발견되어 새 계정으로 돈을 보내는 거래에 사용되었음을 의미한다. 블록체인 데이터는 변경할 수 없으므로, 개인키를 훔치고 자산을 이체한다면 해당 거래를 취소하는 것은 불가능하다.

### 원장

- 트랜잭션의 모음이다.
- 블록체인 네트워크는 설계에 따라 분산되어 각 피어 간에 동일한 원장 데이터를 업데이트하고 동기화하는 많은 복사본을 생성한다. 새로운 노드가 블록체인 네트워크에 합류할 때마다 다른 노드를 찾아 블록체인 네트워크 원장의 전체 사본을 요청하여 원장의 손실이나 파괴를 어렵게 한다.
- 블록체인 네트워크는 SW, HW, 그리고 네트워크 인프라가 모두 다른 이기종 네트워크이다. 블록체인 네트워크 노드 사이에는 많은 차이점이 있기 때문에 하나의 노드에 대한 공격이 다른 노드에서도 작동한다는 보장이 없다.
- 블록체인 네트워크는 전 세계에서 지리적으로 다양한 노드로 구성된다. P2P 방식으로 작동하는 블록체인 네트워크는 손실에 대해 탄력적이다.
- 블록체인 네트워크는 모든 거래(트랜잭션)이 유효한지 확인해야 한다. 악의적인 노드가 트랜잭션을 전송하면 다른 사람들이 이를 감지하고 무시하여 잘못된 트랜잭션이 전파되는 것을 방지한다.
- 블록체인 네트워크는 분산 원장 내에서 수락된 모든 트랜잭션을 보유한다. 새 블록을 구축하기 위해 이전 블록을 참조해야 하므로 게시 노드에 최신 블록에 대한 참조가 포함되어 있지 않으면, 다른 노드는 이를 거부한다.
- 블록체인 네트워크는 디지털 서명 및 암호화 해시 가능을 사용하여 변조 방지를 제공한다.
- 일반적으로 블록체인 네트워크의 정보는 공개적으로 볼 수 있으며, 훔칠 것이 없다. 블록체인 네트워크의 사용자를 공격하려면 개별적으로 대상을 지정해야 한다. 또한, 블록체인 자체를 공격에 대한 목표로 하는 것은 신뢰성 있는 노드의 저항에 부딪힌다.

### 블록

- 블록체인 네트워크의 사용자는 블록체인 네트워크에 후보 트랜잭션을 제출한다. 제출된 트랜잭션을 다른 노드로 전파하지만, 블록화 하지는 않는다. 게시 노드가 블록을 게시할 때 트랜잭션이 블록체인에 추가된다. 블록 헤더에는 이 블록에 대한 메타데이터가 포함된다.
- 블록 데이터에는 블록체인 네트워크에 제출된 검증되고 인증된 트랜잭션 목록이 포함된다. 트랜잭션의 형식이 올바르고 각 트랜잭션의 디지털 자산 제공자가 각각 암호화된 트랜잭션에 서명하였는지 확인하여 유효성과 신뢰성을 보장한다. 이를 통해 거래에 대한 디지털 자산 제공자가 사용 가능한 디지털 자산에 서명할 수 있는 개인키를 보유하는 지 확인한다.
- 다른 전체 노드는 게시된 블록에 있는 모든 트랜잭션의 유효성과 신뢰성을 확인하고, 유효하지 않은 트랜잭션이 포함된 블록은 수락하지 않는다.

#### 블록의 구조

##### 블록 헤더

- The block number, also known as block height in some blockchain networks.
- The previous block header’s hash value.
- A hash representation of the block data (different methods can be used to accomplish this, such as a generating a Merkle tree, and storing the root hash, or by utilizing a hash of all the combined block data).
- A timestamp.
- The size of the block.
- The nonce value. For blockchain networks which utilize mining, this is a number which is manipulated by the publishing node to solve the hash puzzle. Other blockchain networks may or may not include it or use it for another purpose other than solving a hash puzzle.

##### 블록 데이터

- A list of transactions and ledger events included within the block.
- Other data may be present.

## 블록체인 기술 기초 공부 참고문헌

- https://arxiv.org/abs/1906.11078
- https://www.youtube.com/watch?v=bBC-nXj3Ng4
