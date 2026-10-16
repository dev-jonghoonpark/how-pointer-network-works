# How Pointer Network Works

**Pointer Networks — 어텐션으로 입력을 가리키기.** Pointer Networks(Vinyals·Fortunato·Jaitly, NeurIPS 2015)를 브라우저에서 직접 실험하며 이해하는 인터랙티브 교육 자료입니다. 답이 “입력의 몇 번째”인 문제에서 seq2seq의 출력층이 왜 막히는지, 어텐션 분포로 인코더 상태를 섞지 않고 **그 분포를 그대로 출력으로 쓰면** 출력 사전이 입력 길이에 맞춰 저절로 늘어난다는 것을 확인합니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-pointer-network-works/)**

## 다루는 내용

0. **먼저: 볼록 껍질이란?** · 고무줄 비유로 보는 꼭짓점과 안쪽 점, 출력 번호열(⇒ 3 → 6 → 4 → 5 → 3 ⇐, 시작점을 한 번 더 적어 닫기)의 표기 규칙, 이 문제가 첫 과제가 된 이유
1. **출력할 칸이 미리 정해져 있다** · n = 5로 학습한 seq2seq가 점 7개의 볼록 껍질에서 “6번”을 말할 수 없는 것
2. **정답이 ‘입력의 번호’인 문제들** · 점을 찍고 끌며 보는 볼록 껍질과 TSP 출력 번호열(Held-Karp 최적해 vs 최근접 이웃 탐욕법), 논문의 출력 표기 규칙
3. **어텐션을 섞지 말고 가리키게** · 논문 식 (3)과 Ptr-Net 식 비교, 가중 평균 d′는 늘 입력 사이 어딘가이고 포인터는 반드시 입력 중 하나라는 2D 데모
4. **한 스텝씩 따라가기** · 0절 그림의 점 7개를 스텝마다 디코딩하며 보는 선택 메커니즘 — 자연어 생성처럼 매 스텝 다음 점 하나를 고르고, 직전에 고른 점이 디코더 상태(질의)만 바꾸며, 안쪽 점 P1·P2·P7은 지워지는 게 아니라 끝까지 후보로 남지만 학습된 점수가 낮아 뽑히지 않는다는 것. 디코더 상태로 배우는 방식(원 논문)과 마스크(후속 연구)의 차이
5. **브라우저에서 학습하는 미니 Ptr-Net** · 파라미터 96개짜리 포인터가 정렬을 배우는 과정을 스텝×입력 확률 행렬로 보기
6. **같은 가중치로 더 긴 입력 — 그리고 마스크** · 길이 5~10으로 학습해 50까지 평가, 마스크를 끄면 같은 위치를 또 가리키는 출력이 늘어나는 것(논문이 TSP 빔 서치를 유효 경로로 제한한 이유)
7. **논문 실험 결과** · 볼록 껍질(표 1), 들로네 삼각분할, TSP(표 2) — A1 데이터로 배워 A1보다 짧은 경로를 낸 결과
8. **그다음: 복사하는 포인터** · pointer-generator의 p<sub>gen</sub> 슬라이더로 보는 OOV 단어 복사, CopyNet·Pointer Sentinel·RL로 푸는 TSP
9. **퀴즈** 7문항

## 참고

- Vinyals, Fortunato, Jaitly (2015), *Pointer Networks* — [arXiv:1506.03134](https://arxiv.org/abs/1506.03134)
- Bahdanau, Cho, Bengio (2014), *Neural Machine Translation by Jointly Learning to Align and Translate* — [arXiv:1409.0473](https://arxiv.org/abs/1409.0473)
- See, Liu, Manning (2017), *Get To The Point: Summarization with Pointer-Generator Networks* — [arXiv:1704.04368](https://arxiv.org/abs/1704.04368)

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.
