# paperReview

컴퓨터 과학, 그중에서도 주로 딥러닝 관련 논문을 읽고 그 내용을 간략하게 정리한 레포입니다.
간단하게 읽은 논문은 모두 이 레포에 저장되고 그중에서도 중요한 내용은 자세히 정리하여 티스토리나 유튜브 영상으로 업로드할 예정입니다.

### paper list

현재까지 리뷰한 논문/자료의 목록은 아래와 같습니다.

- [x] webb-c/paperReview#3 Optimal Control of Distributed Computing Networks with Mixed-Cast Traffic Flows (INFOCOM 2018)
  - [Original Paper Link](https://ieeexplore.ieee.org/document/8485956) / Paper Review Post / Paper Review Video
- [x] webb-c/paperReview#4 FrameHopper: Selective Processing of Video Frames in Detection-driven Real-Time Video Analytics (DCOSS 2022)
  - [Original Paper Link](https://ieeexplore.ieee.org/abstract/document/9881637) / Paper Review Post / Paper Review Video
- [x] ~~webb-c/paperReview#1 The MAXQ Method for Hierarchical Reinforcement Learning (Journal of artificial intelligence research 1998)~~
  - [Original Paper Link](https://arxiv.org/abs/cs/9905014) / Paper Review Post / Paper Review Video
- [x] ~~webb-c/paperReview#2 Data-Efficient Hierarchical Reinforcement Learning (NeurIPS 2018)~~
  - [Original Paper Link](https://arxiv.org/abs/1805.08296) / Paper Review Post / Paper Review Video
- [x] webb-c/paperReview#5 Hindsight Experience Replay (NeurIPS 2017)
  - [Original Paper Link](https://arxiv.org/abs/1707.01495) / Paper Review Post / Paper Review Video
- [x] webb-c/paperReview#6 RUDDER: Return Decomposition for Delayed Rewards (NeurIPS 2019)
  - [Original Paper Link](https://arxiv.org/abs/1806.07857) / Paper Review Post / Paper Review Video
- [ ] webb-c/paperReview#7 Optimal Control for Generalized Network-Flow Problems (IEEE/ACM Transactions on Networking 2018)
  - [Original Paper Link](https://ieeexplore.ieee.org/abstract/document/8241883) / Paper Review Post / Paper Review Video
- [ ] webb-c/paperReview#8 Policy Learning with Constraints in Model-free Reinforcement Learning A Survey (IJCAI 2021)
  - [Original Paper Link](https://par.nsf.gov/biblio/10313521) / Paper Review Post / Paper Review Video
- [ ] webb-c/paperReview#9 Infinitely often, Probability 1, Borel-Cantelli, and the Law of Large Numbers
  - [Original Paper Link](https://viterbi-web.usc.edu/~mjneely/Borel-Cantelli-LLN.pdf) / Paper Review Post / Paper Review Video
<br>

---

### Template

논문 리뷰에 사용하는 템플릿은 아래와 같습니다.

```
# paper Title

#### Link

[]()

#### Information

- Author/Institution :
- Conference/Journal :
- Cited by _ _(YYYY.MM.DD)_
- Submitted on Day Month Year

## Abstract
논문의 전반적인 내용을 요약한다.
- 세 줄
- 요
- 약

## comparison with Related Work
다른 연구와 이 논문에서 진행한 연구만의 장점, 다른 점을 설명한다.

## Key point
논문의 주요 아이디어나 새로운 방안에 대해 설명한다.

## Algorithm
논문의 알고리즘을 설명한다.

## Formulation
수식에 대한 설명이 중요한 논문인 경우, formulation을 함께 정리한다.

## Insight
논문을 통해 얻어가는 것들이나 생각해 낸 아이디어를 간략히 기술한다.
```

---

### Commit Rules

커밋 규칙은 아래와 같습니다.

`new : 논문 이름` : 읽을 논문 issue 등록  
`add : 논문 이름` : 논문 리뷰 파일(`.md`) 추가 & README 정보 업데이트  
`add+ : 논문 이름` : 특정 논문 리뷰 티스토리 업로드  
`add++ : 논문 이름` : 특정 논문 리뷰 유튜브 업로드  
`update : 논문 이름` : 첫 논문 리뷰 등록 이후 수정
