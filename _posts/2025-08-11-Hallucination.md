---
title:  "[논문 리뷰] Understading Hallucinations in Diffusion Models through Mode Interpolation"
excerpt: "Diffusion에서 일어나는 hallucination에 대한 논문 리뷰"

toc: true
toc_sticky: true

categories:
  - ComputerVision 
  - PaperReview
  - MultiModal

use_math: true
header:
  teaser: https://i.ibb.co/GQsqWcH2/thumbnails.jpg

---

> Aithal, Sumukh K and Maini, Pratyush and Lipton, Zachary C and Zico Kolter, J

논문 <font style="color:hsl(27, 100%, 43%)">Understanding Hallucinations in Diffusion Models through Mode Interpolation</font>을 읽고, 
최대한 다른 분들이 보셨을 때 이해가 잘 되도록 요약 및 핵심 내용 설명 위주로 Paper Review를 진행할 예정입니다.

본 논문은 현재 아카이브에 기재되어 있으며, 그동안의 Diffusion model에서의 **hallucination**에 대한 해결 방법으로 데이터 증강을 사용하거나 모델 크기를 키웠던 반면, 본 논문에서는 <font style="color:hsl(27, 100%, 43%)">Diffusion decoder에서 일어나는 mode interpolation 관점</font>으로 다루고 있어 소개해보았습니다.

논문에서의 순서를 일정하게 지키는 것보다, 각 목차에서 필요할 것 같다 생각하는 부분을 먼저 언급하거나, 뒷 부분에서 언급할 수 있습니다. 보시고 피드백도 자유롭게 주셨으면 좋겠습니다!

<br>

## 🥸 Hallucination이란?

### Hallucination의 정의

<font style="color:hsl(27, 100%, 43%)">Hallucination</font>이란, 훈련 데이터에서 한 번도 일어난 적 없던 샘플이 만들어지는 현상입니다. 모델이 생성한 샘플이 실제 데이터 분포의 지지집합(support) 밖에 완전히 위치하는 경우인 것이죠.

이러한 현상은 <font style="color:hsl(27, 100%, 43%)">mode interplation</font>이 발생할 때 생기는데, 본 논문에서는 diffusion 모델이 데이터 분포의 **인접한 두 mode 사이를 보간**하여 hallucination을 생성하는 경향이 있다는 것을 주장합니다.

<center><img src="https://github.com/user-attachments/assets/8de81e01-638a-43bf-acac-6bfb57806c57" width="70%"></center>

<br>

## 🔎 Mode Interpolation의 원인

### Score Function의 분

Instruction tuning은 fine-tuning과 비슷한 듯, 다른 개념입니다. 다양한 주제에 대한 **instruction-task 쌍**을 사용하여 학습하기 때문에, 다양한 작업에서도 zero shot이 가능합니다.

반면 fine-tuning은 **task-specific한 데이터**를 갖고 학습하기 때문에, 특정 작업에 특화되어 있으며, 다른 작업의 경우 해당 작업에 맞는 데이터셋으로 **재학습**이 필요합니다.

<center><img src="https://github.com/user-attachments/assets/66a85cbb-7ed7-46a0-afc0-1c89d5e59276" width="80%"></center>

<br>

### Instruction tuning의 multi-modal 모델로의 확장

Instruction tuning은 보통 text 기반이었으며, **Image-text 쌍** 데이터를 학습하여 훈련한 Flamingo나 BLIP-2같은 모델들은 이미지를 설명하는 것에만 그쳐 더 **복잡한 지시 추론 능력**(<font style="color:hsl(27, 100%, 43%)">instruction-following</font>)이 부족했습니다.

별도로 LLaMA와 같은 오픈소스 **LLM**을 **multi-modal**로 확장하려는 시도가 이뤄지고 있지만, **Vsion-language instruction data**를 사용해 tuning되지 않아 multi-modal 입력에 대한 성능은 낮습니다. (⇢ language 입력에 대한 성능과 별반 다르지 않음)

그래서 본 논문에서는 **multi-modal 모델**의 <font style="color:hsl(27, 100%, 43%)">instruction-following</font> 능력을 개선하는 것을 목표로 <font style="color:hsl(27, 100%, 43%)">Visual instruction tuning</font>을 새롭게 시도하였습니다. 즉 instruction tuning을 <font style="color:hsl(27, 100%, 43%)">language-image</font> 공간으로 확장한 **첫 번째** 시도를 하게 된 것입니다.

<br>

## 🔭 Overview

### Object
- **LLaVA 모델** 개발 : multi-modal 모델 'LLaVA(Large Langugae and Vision Assistant)' 개발하였습니다.
- **Visual Instruction Tuning** 도입 : 사용자의 구체적인 지시를 이해하고 수행할 수 있는 instruction-following 성능을 개선했습니다.

### Contribution
- **Multi-modal instruction following data** 구축 : GPT-4를 사용하여 기존 데이터를 새롭게 instruction 형식으로 전환하여 구축하였으며, 이를 위한 pipeline을 제시했습니다.
- Large multi-modal 모델인 **LLaVA** 개발 : GPT-4와 결합시, ScienceQA에서 SOTA를 달성하였습니다.
- 최초의 **Multi-modal instruction-following benchmark**를 제안하였습니다.

<br>

## 📜 Methodology

### GPT-assisted Visual Instruction Data Generation

현재 mutli-modal 데이터는 많아진 반면, instruction-following 데이터는 여전히 부족한 상황입니다. 인간이 참여하는 데이터 수집은 오랜 시간이 필요하며, 구체적인 정의가 부족하기 때문입니다. 그래서 본 논문에서는 기존 **image-text 쌍 데이터**를 <font style="color:hsl(27, 100%, 43%)">instruction-following 형식</font>으로 확장하여 데이터를 생성하고자 합니다.

#### <1> 첫 번째 방법

**Image $$X_v$$**와 그에 맞는 **caption $$X_c$$**를 통해 이미지 설명을 유도하는 **질문 집합 $$X_q$$**로 데이터셋을 생성합니다.

$$
Human:X_qX_v<STOP> Assistant:X_c<STOP>
$$

이렇게 데이터를 생성하면, 비교적 간단하기 때문에 저비용으로 생성이 가능하지만, **다양성이 부족**하며, 깊이 있는 reasoning이 어렵습니다.

<br>

#### <2> 새로운 방법

그리하여 **Image-text 쌍** 데이터를 기반으로 <font style="color:hsl(27, 100%, 43%)">GPT-4나 ChatGPT</font>를 활용하여 생성하는 방법을 고안하였습니다.
그러나 문제는 다음과 같습니다.

1. Text-only GPT-4나 ChatGPT가 **visual content**를 인지할 수 없는 문제
2. 다양한 Instruction-following 데이터의 형태

이를 본 논문에서는 모두 해결하여 데이터를 생성하였습니다.

<br>

#### ✅ Symbolic representation (프롬프 입력)

첫 번째 문제인 Language-only LLM이 visual content를 인지할 수 없는 문제의 해결방안인 <font style="color:hsl(27, 100%, 43%)">Symbolic representation</font>입니다. 이 방법은 이미지를 '**텍스트**'로 표현(<font style="color:hsl(27, 100%, 43%)">encoding</font>)하여 GPT-4와 ChatGPT에 활용하기 위하여 사용됩니다. Symbolic representation을 위한 context type은 총 2가지이며 지금부터 알아보겠습니다.

Context type 1. **Captions**
- 시각 장면(image scene)을 다양한 관점에서 설명하는 데 유용합니다.
<center><img src="https://github.com/user-attachments/assets/7cb13571-a3c5-47e8-975d-e56a48d61465" width="85%"></center>

<p>

Context type 2. **Bounding boxes**
- 장면 내 **객체의 위치**를 설명할 때 사용됩니다.
<center><img src="https://github.com/user-attachments/assets/ea9ced9d-e5c9-400e-98e4-422305c0433f" width="85%"></center>

<br>

#### ✅ Instruction-following 데이터를 구성하기 위한 Response

위 context를 통해 이미지(visual content)를 LLM이 인지할 수 있도록 인코딩 했다면, COCO 이미지를 사용하여 3가지 유형의 instruction-following 데이터를 생성합니다.

Response type 1. **Conversation**
- user(사람)과 **assistant 간의 대화**를 디자인한 것입니다. assistant가 이미지를 보고 답변하는 것과 같이 구성되어 있습니다.
- 물체 유형, 개수, 동작, 위치, 상대적 위치 등 이미지의 시각적 내용에 대한 확실한 답변이 있는 질문이 제기됩니다.
- 다음은 생성된 conversation입니다.
<center><img src="https://github.com/user-attachments/assets/2aeb4188-09ff-414b-a0a9-a78a0b5574ff" width="85%"></center>

<p>

Response type 2. **Detailed description**
- 이미지에 대한 **상세한 설명**을 생성합니다.
- 다음 이미지의 질문 목록에서 하나의 질문을 무작위로 골라 GPT-4에게 이미지에 대한 자세한 설명을 생성하도록 요청합니다.
<center><img src="https://github.com/user-attachments/assets/15f68471-3c4e-4711-a12c-a4890cb8285a" width="65%"></center>

- 만들어진 description은 다음과 같습니다.
<center><img src="https://github.com/user-attachments/assets/33a41a78-6340-4a24-9379-a497c36369ad" width="85%"></center>

<p>

Response type 3. **Complex reasoning**
- 심층적인 **추론**을 하는 질문 및 답변으로 구성되며, 답변에는 **단계별로 논리가 포함**된 이유가 함께 필요합니다.
- 다음은 complex reasoning입니다.

<center><img src="https://github.com/user-attachments/assets/de46f176-4451-4c36-a023-a33af4cef77a" width="85%"></center>

<p>

이렇게 3가지 response type에 대해 총 **158,000개**의 데이터를 생성할 수 있었습니다.

<br>

### LLaVA 모델 아키텍처
사전 학습된 **LLM**과 사전 학습된 **visual model**을 효과적으로 활용하는 것이 목표이며, 공개된 체크 포인트 중 instruction-following 능력이 가장 뛰어난 모델을 사용하여 구성하였습니다.

<center><img src="https://github.com/user-attachments/assets/aeedb374-8f6d-4423-9bbc-1f59dcdd387a" width="75%"></center>

- **Language model** : Vicuna ($$f_\phi$$)
- **Vision encoder** : 사전 학습된 CLIP vision encoder ViT-L/14



<center><img width="75%"></center>