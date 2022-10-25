---
title: 딥러닝/인공지능 - Chatbot 만들기
updated: 2022-10-25 23:07
---

<div class="divider"></div>

### 토크나이징(Tokenizing) 
 > 문장이 들어오면 각 단어를 9품사로 나눠주는 과정

<div class="divider"></div>

### 임베딩(Embedding) 
 > 자연어를 숫자(벡터화)형태로 바꾸는 것

<div class="divider"></div>

### 한국형 토크나이징

> KoNLPy는 3가지 토크나이징 모델을 가지고 있습니다.
* 코랩에서 import하기 

```python
%%bash
apt-get update
apt-get install g++ openjdk-8-jdk python-dev python3-dev
pip3 install JPype1
pip3 install konlpy
```

<div class="divider"></div>

1. komoran - 42개의 품사 태그를 지원

```python
  from konlpy.tag import Komoran
# 코코마 형태소 분석기 객체 생성
komoran = Komoran()

text = "설참해라"

# 형태소 추출
morphs = komoran.morphs(text)
print(morphs)

# 형태소와 품사 태그 추출
pos = komoran.pos(text)
print(pos)

# 명사만 추출
nouns = komoran.nouns(text)
print(morphs)

# 3개 모델중 성능이 가장 별로임
```

```
['설', '참', '하', '아라']
[('설', 'NNG'), ('참', 'NNG'), ('하', 'XSV'), ('아라', 'EC')]
['설', '참', '하', '아라']

```

<div class="divider"></div>

2. kkma - 56개의 품사 태그를 지원

 ```python
  from konlpy.tag import Kkma

# 코코마 형태소 분석기 객체 생성
kkma = Kkma()

text = "가시참피마냥 커엽눜ㅋㅋㅋ"

# 형태소 추출
morphs = kkma.morphs(text)
print(morphs)

# 형태소와 품사 태그 추출
pos = kkma.pos(text)
print(pos)

# 명사만 추출
nouns = kkma.nouns(text)
print(nouns)

# 형태소 추출
sentences = "가시참피마냥 커엽눜ㅋㅋㅋ"
s= kkma.sentences(sentences)
print(s)

## 제일 보통인 모델
 ```

```
['가시', '참', '피', '마냥', '크', '어', '엽', '눜', 'ㅋㅋㅋ']
[('가시', 'NNG'), ('참', 'MAG'), ('피', 'NNG'), ('마냥', 'MAG'), ('크', 'VA'), ('어', 'ECS'), ('엽', 'NNM'), ('눜', 'UN'), ('ㅋㅋㅋ', 'EMO')]
['가시', '피', '엽', '엽눜', '눜']
['가시 참 피 마냥 커 엽 눜 ㅋㅋㅋ']
```

<div class="divider"></div>

3. okt - 트위터에서 만듬 (Open-Source Korean Text Processor)

 ```python
  from konlpy.tag import Okt
# 코코마 형태소 분석기 객체 생성
okt = Okt()

text = "운동을 해도 우울해"

# 형태소 추출
morphs = okt.morphs(text)
print(morphs)

# 형태소와 품사 태그 추출
pos = okt.pos(text)
print(pos)

# 명사만 추출
nouns = okt.nouns(text)
print(morphs)

# 정규화, 어구 추출
print(okt.normalize(text))
print(okt.phrases(text))

## 눜ㅋㅋㅋ, 엌ㅋㅋㅋ 이런 단어를 /누ㅋㅋㅋㅋ, 어ㅋㅋㅋㅋㅋ 로 쉽게 변환됨
 ```
```
['운동', '을', '해도', '우울해']
[('운동', 'Noun'), ('을', 'Josa'), ('해도', 'Noun'), ('우울해', 'Adjective')]
['운동', '을', '해도', '우울해']
운동을 해도 우울해
['운동', '해도']
```

<div class="divider"></div>

### 인베딩 인스톨 하기

```
  pip install gensim

```

* 구글드라이브 안에 데이터셋(웰니스)을 넣고 코랩에서 불러옴 

```python
from google.colab import drive
drive.mount('/content/drive')
```

<div class="divider"></div>

1. komoran 인베딩 하기

```python
from gensim.models import Word2Vec
from konlpy.tag import Komoran
import pandas as pd
import time

# 학습 시간 측정 시작
start = time.time()

# 웰니스 데이터 읽어오기
print("1) 말뭉치 데이터 읽기 시작")
wellness_data=pd.read_excel('/content/drive/MyDrive/hackerton/wellness.xlsx')
print(len(wellness_data))
print(" 1) 말뭉치 데이터 읽기 완료: ", time.time() - start)

# 문장 단위로 명사만 추출해 학습 입력 데이터로 만듦
print(" 2) 형태소에서 명사만 추출 시작")
komoran = Komoran()
docs_wellness_Komoran = []

# 엑셀 컬럼 기준으로 데이터로 가져옴
for i in wellness_data['utterance(2차) '].unique():
  if not pd.isnull(i):
    docs_wellness_Komoran.append(i)

# 가져온 데이터를 komoran으로 쪼게버리기~
docs_wellness_Komoran = [komoran.nouns(sentence) for sentence in docs_wellness_Komoran]
print(" 2) 형태소에서 명사만 추출 완료: ", time.time() - start)

# Word2Vec 모델 학습
print(" 3) Word2Vec 모델 학습 시작")
model_wellness_komoran = Word2Vec(sentences=docs_wellness_Komoran, size= 200, window=4, hs=1, min_count=2, sg=1)
print(" 3) Word2Vec 모델 학습 완료:", time.time() - start)

# 모델 저장
print(" 4) 모델 저장 시작")
model_wellness_komoran.save("wellness_komoran.model")
print(" 4) 모델 저장 완료:", time.time() - start)

# 학습된 말뭉치 수, 코퍼스 내 전체 단어 수
print("corpus_count :", model_wellness_komoran.corpus_count)
print("corpus_total_word : ", model_wellness_komoran.corpus_total_words)

```

모델 학습결과

```
1) 말뭉치 데이터 읽기 시작
19769
 1) 말뭉치 데이터 읽기 완료:  3.0705180168151855
 2) 형태소에서 명사만 추출 시작
 2) 형태소에서 명사만 추출 완료:  18.518791913986206
 3) Word2Vec 모델 학습 시작
 3) Word2Vec 모델 학습 완료: 19.934099435806274
 4) 모델 저장 시작
 4) 모델 저장 완료: 21.753016710281372
corpus_count : 19672
corpus_total_word :  54976
```

Word2Vec 모델 활용

```python
from gensim.models import Word2Vec

# 모델 로딩
model_wellness_komoran = Word2Vec.load("wellness_komoran.model")
print("corpus_total_word : ", model_wellness_komoran.corpus_total_words)

# '사랑'이란 단어로 생성한 단어 임베딩 벡터
print("우울: ", model_wellness_komoran.wv['우울'])

# 단어 유사도 계산
print("우울 = 불안\t", model_wellness_komoran.wv.similarity(w1="우울", w2="불안"))
print("우울 = 압박\t", model_wellness_komoran.wv.similarity(w1="우울", w2="압박"))
print("공허 = 눈물\t", model_wellness_komoran.wv.similarity(w1="멍", w2="눈물"))
print("행복 != 불안\t", model_wellness_komoran.wv.similarity(w1="행복", w2="불안"))
print("진정 != 우울\t", model_wellness_komoran.wv.similarity(w1="진정", w2="우울"))

# 가장 유사한 단어 추출
print(model_wellness_komoran.wv.most_similar("우울", topn=5))
print(model_wellness_komoran.wv.most_similar("공허", topn=5))

# >> komoran은 공허를 못찾음 >> 토큰나이징이 잘 안됨
```

Word2Vec 모델 활용 결과

```python
corpus_total_word :  54976
우울:  [-7.48126134e-02  3.35401967e-02 -7.13696703e-02 -1.23185620e-01
  7.94638246e-02 -4.45739590e-02  1.08325638e-01 -1.27068684e-01
 -5.95277026e-02 -5.62046170e-02 -5.91871189e-03  6.38181064e-03
 -1.66367292e-02  1.63625821e-01 -6.75797090e-02 -1.43452492e-02
  7.99940899e-02  2.54921112e-02  2.30818074e-02 -1.01856902e-01
 -1.52239412e-01  1.16290804e-03  1.32875264e-01  4.92461026e-02
  3.72202359e-02  5.42255081e-02  1.16991371e-01 -1.48181856e-01
  1.15198351e-01  1.24267275e-02  7.18855113e-02 -2.63264209e-01
  1.33473441e-01 -1.09358355e-01  4.44466306e-04  3.24270129e-02
  7.05165714e-02 -1.96918063e-02 -1.59707572e-02 -2.40671933e-02
 -1.27084479e-01  1.14169709e-01 -2.30349228e-02  7.77057745e-03
 -4.89576310e-02 -1.74751475e-01  2.07979400e-02  4.41149101e-02
  8.01817998e-02 -1.39721364e-01 -1.29125223e-01 -7.69721717e-02
  5.15309125e-02  3.35278735e-02 -8.46843421e-03  5.50417937e-02
  8.89077559e-02 -1.89775396e-02  1.08437121e-01 -1.52911648e-01
 -1.19999021e-01  1.35371819e-01  2.18095002e-03 -4.64865305e-02
  8.72924030e-02  1.77762955e-02 -5.61625622e-02 -3.34957335e-03
 -2.13318184e-01 -2.81186067e-02  9.94120464e-02  3.78026888e-02
 -1.37378037e-01  8.42920244e-02  9.16531309e-02  6.14449084e-02
 -7.29762986e-02  6.89971894e-02 -1.64645597e-01  3.45996208e-03
 -3.64947692e-02  8.13145339e-02  1.03136845e-01 -6.03765212e-02
  6.41075149e-02 -5.74801676e-03  1.10423893e-01 -1.51981320e-02
  1.04509607e-01 -1.07411623e-01  1.43438742e-01  1.65631194e-02
 -7.54391253e-02 -1.66200340e-01 -1.79804936e-02  1.04174316e-01
 -2.63467804e-02  1.00980841e-01 -2.03736603e-01 -3.90588492e-02
  9.33660641e-02 -9.84034985e-02  1.34809732e-01 -1.63143322e-01
 -5.05454242e-02 -7.50286970e-03 -7.23978058e-02 -8.44271109e-02
  1.75050212e-04  8.08248892e-02 -7.97789916e-02  1.89797562e-02
  8.07472393e-02  1.61523931e-02 -5.38539290e-02 -8.24461225e-03
 -2.33646885e-01 -4.57919501e-02  6.19689450e-02  9.96909197e-03
  1.01249062e-01 -1.42542720e-01  3.62093709e-02  1.08592501e-02
 -1.88402355e-01  2.57353216e-01 -3.53776328e-02 -7.14356825e-02
 -5.98780252e-02 -7.69841392e-03 -5.33369705e-02  1.21671036e-02
 -1.53716560e-02  2.43681759e-01  1.22683689e-01  1.83737770e-01
  4.45007533e-02 -1.97525658e-02  7.64366984e-02  9.34008285e-02
 -9.78832990e-02  1.32840723e-01 -9.74838808e-02  6.59481138e-02
  2.32621431e-02  1.29910395e-01 -4.63240370e-02 -4.60609868e-02
 -1.12155371e-03  2.69764662e-02  4.59618968e-05 -1.83838189e-01
  6.83884397e-02  5.91610298e-02  1.23127826e-01  1.21771388e-01
  3.89400572e-02 -2.27012634e-02  2.02455834e-01  1.64818183e-01
  1.84375606e-02 -6.36797026e-02 -2.47402787e-01 -3.29077616e-02
 -1.57315910e-01  1.87400535e-01  6.15734346e-02 -2.29254782e-01
  2.47177258e-01  4.13745344e-02 -2.07496658e-02 -6.05641007e-02
 -1.15899570e-01  1.60706460e-01  1.58716798e-01 -9.95811000e-02
 -6.42380044e-02  1.09091982e-01 -6.22800700e-02  1.24150731e-01
 -6.87899739e-02 -9.77091584e-03  8.77170265e-02  6.84699491e-02
  6.40999600e-02  9.25477892e-02  8.22909325e-02 -6.21349551e-02
  1.32362336e-01  7.63870105e-02  8.62266310e-03  1.00332499e-01
 -6.68020323e-02  3.97708034e-03 -6.94536939e-02  7.17507210e-03
  4.52874824e-02 -1.04062788e-01  5.24830744e-02  5.50097302e-02]
우울 = 불안	 0.8730131
우울 = 압박	 0.89442426
공허 = 눈물	 0.80701536
행복 != 불안	 0.9163255
진정 != 우울	 0.83750206
[('상태', 0.9569607377052307), ('컨디션', 0.9507994055747986), ('학교', 0.9506539106369019), ('준비', 0.9489731788635254), ('얼마', 0.9449964165687561)]
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-8-cb0b84b9f322> in <module>
     17 # 가장 유사한 단어 추출
     18 print(model_wellness_komoran.wv.most_similar("우울", topn=5))
---> 19 print(model_wellness_komoran.wv.most_similar("공허", topn=5))

1 frames
/usr/local/lib/python3.7/dist-packages/gensim/models/keyedvectors.py in word_vec(self, word, use_norm)
    450             return result
    451         else:
--> 452             raise KeyError("word '%s' not in vocabulary" % word)
    453 
    454     def get_vector(self, word):

KeyError: "word '공허' not in vocabulary"
```

<div class="divider"></div>

2. komoran 인베딩 하기

```python
from gensim.models import Word2Vec
from konlpy.tag import Kkma
import pandas as pd
import time

# 학습 시간 측정 시작
start = time.time()

# 웰니스 데이터 읽어오기
print("1) 말뭉치 데이터 읽기 시작")
wellness_data=pd.read_excel('/content/drive/MyDrive/hackerton/wellness.xlsx')
print(len(wellness_data))
print(" 1) 말뭉치 데이터 읽기 완료: ", time.time() - start)

# 문장 단위로 명사만 추출해 학습 입력 데이터로 만듦
print(" 2) 형태소에서 명사만 추출 시작")
kkma = Kkma()
docs_wellness_kkma = []

# 엑셀 컬럼 기준으로 데이터로 가져옴
for i in wellness_data['utterance(2차) '].unique():
  if not pd.isnull(i):
    docs_wellness_kkma.append(i)

# 가져온 데이터를 kkma으로 쪼게버리기~
docs_wellness_kkma = [kkma.nouns(sentence) for sentence in docs_wellness_kkma]
print(" 2) 형태소에서 명사만 추출 완료: ", time.time() - start)

# Word2Vec 모델 학습
print(" 3) Word2Vec 모델 학습 시작")
model_wellness_kkma = Word2Vec(sentences=docs_wellness_kkma, size= 200, window=4, hs=1, min_count=2, sg=1)
print(" 3) Word2Vec 모델 학습 완료:", time.time() - start)

# 모델 저장
print(" 4) 모델 저장 시작")
model_wellness_kkma.save("wellness_kkma.model")
print(" 4) 모델 저장 완료:", time.time() - start)

# 학습된 말뭉치 수, 코퍼스 내 전체 단어 수
print("corpus_count :", model_wellness_kkma.corpus_count)
print("corpus_total_word : ", model_wellness_kkma.corpus_total_words)
```

모델 학습결과

```
1) 말뭉치 데이터 읽기 시작
19769
 1) 말뭉치 데이터 읽기 완료:  3.3066468238830566
 2) 형태소에서 명사만 추출 시작
 2) 형태소에서 명사만 추출 완료:  419.34420943260193
 3) Word2Vec 모델 학습 시작
 3) Word2Vec 모델 학습 완료: 422.3020739555359
 4) 모델 저장 시작
 4) 모델 저장 완료: 424.21959114074707
corpus_count : 19672
corpus_total_word :  57913
```

Word2Vec 모델 활용

```python
from gensim.models import Word2Vec

# 모델 로딩
model_wellness_kkma = Word2Vec.load("wellness_kkma.model")
print("corpus_total_word : ", model_wellness_kkma.corpus_total_words)

# '사랑'이란 단어로 생성한 단어 임베딩 벡터
print("우울: ", model_wellness_kkma.wv['우울'])

# 단어 유사도 계산
print("우울 = 불안\t", model_wellness_kkma.wv.similarity(w1="우울", w2="불안"))
print("우울 = 압박\t", model_wellness_kkma.wv.similarity(w1="우울", w2="압박"))
print("공허 = 눈물\t", model_wellness_kkma.wv.similarity(w1="멍", w2="눈물"))
print("행복 != 불안\t", model_wellness_kkma.wv.similarity(w1="행복", w2="불안"))
print("진정 != 우울\t", model_wellness_kkma.wv.similarity(w1="진정", w2="우울"))

# 가장 유사한 단어 추출
print(model_wellness_kkma.wv.most_similar("우울", topn=5))
print(model_wellness_kkma.wv.most_similar("공허", topn=5))

# >> kkma은 생각보다 정서적인 측면에서 잘 맞는 듯
```

Word2Vec 모델 활용 결과

```python
corpus_total_word :  57913
우울:  [ 4.84883152e-02  7.95987695e-02 -1.18561953e-01  1.36733111e-02
  1.71339273e-01  8.83730277e-02  3.14754508e-02  4.72396752e-03
  4.89911549e-02 -3.28107104e-02 -9.04667564e-03  5.96015453e-02
  2.14637741e-01  5.65396510e-02 -4.80145402e-02 -9.16442648e-02
  2.16947794e-02 -1.70190930e-02  1.70406420e-02 -1.35005847e-01
 -1.15520574e-01  4.98166941e-02  2.25900322e-01 -6.40614033e-02
  9.14278324e-04 -1.23528220e-01  4.58464846e-02 -2.99095184e-01
  1.51577815e-01 -6.14609709e-03 -3.26501355e-02 -1.98712781e-01
  7.63128698e-02 -1.46896914e-01  1.64665490e-01  1.15484089e-01
  1.45497188e-01 -1.92614160e-02 -6.79658949e-02  4.93768044e-02
 -6.39396906e-02  1.09169796e-01 -8.69048107e-03 -5.56037985e-02
  1.61867589e-02 -1.74938917e-01  3.79086845e-02 -9.71052982e-03
 -1.06609156e-02 -3.00934732e-01 -1.48308173e-01 -7.48770088e-02
  9.26457867e-02  1.46017745e-01 -2.67942455e-02  1.90301910e-01
  4.37142886e-03 -6.14804737e-02  6.65865764e-02 -9.88323763e-02
 -1.10486746e-02  1.81947231e-01 -2.23080162e-02 -1.40165970e-01
  1.69757426e-01  1.29478350e-02 -1.37997791e-01 -3.90440263e-02
 -2.79646486e-01  4.53465320e-02  2.26126671e-01  2.38222140e-03
 -7.64013380e-02  1.88322827e-01 -1.15882017e-01  5.74482568e-02
 -1.80931211e-01  1.05643399e-01 -3.05761188e-01 -1.24412276e-01
 -4.82678488e-02  1.42731756e-01  1.64671555e-01 -5.66714145e-02
  1.09424971e-01  1.42099008e-01  2.18868896e-01 -1.21754296e-02
  7.91133940e-03 -5.55250309e-02  6.10416010e-02  1.73492417e-01
  1.98542893e-01 -2.48158365e-01  7.41380826e-02  1.02026634e-01
 -5.84485494e-02 -2.50309445e-02 -1.54339105e-01 -8.30681622e-02
  1.01307727e-01 -1.42959550e-01  5.49914651e-02 -6.84767291e-02
 -6.47371784e-02  1.36823177e-01  4.27270904e-02 -4.37216796e-02
 -1.82902217e-01 -1.34160966e-01 -4.16141860e-02  1.27245542e-02
  1.43133074e-01  8.60273547e-04 -1.49871215e-01 -5.71860932e-02
 -7.02423900e-02 -2.40181070e-02  4.37672436e-02  3.41821127e-02
  1.61919430e-01 -1.15246959e-01  5.20026907e-02  1.39823705e-01
 -3.29883218e-01  2.81777650e-01 -1.08439244e-01 -5.90788350e-02
  1.33876894e-02 -1.81651842e-02 -1.80578262e-01  1.63381770e-02
 -1.00297302e-01  3.27784956e-01  3.22795036e-04  2.68499821e-01
 -8.14224929e-02  7.77355656e-02  1.16147704e-01  2.11329669e-01
  5.38152903e-02  7.71919563e-02 -1.24474108e-01  6.15179613e-02
  1.25553012e-01  1.00761317e-02 -4.09144722e-02  1.41804582e-02
  5.43099549e-03 -3.63545418e-02  2.77818721e-02 -2.46950626e-01
  1.85870200e-01  1.67613745e-01  7.79605806e-02 -9.88971069e-02
  2.52433075e-03 -7.02363625e-02  2.29618207e-01  2.26898476e-01
  9.36033763e-03  1.70816466e-01 -1.16966799e-01 -5.88131808e-02
  1.29620535e-02  6.66330382e-02  2.84946244e-02 -1.85284004e-01
  3.26413624e-02  6.18440770e-02  4.47176434e-02 -1.05073527e-02
  8.06276426e-02  8.69117305e-02  7.63404276e-03 -9.68615189e-02
 -9.59522352e-02  2.40347516e-02 -1.49158284e-01  1.65616602e-01
  5.09314165e-02  2.35601384e-02  3.12368050e-02  6.88796639e-02
  3.43346559e-02 -1.11308731e-01  3.49186212e-02 -4.48124893e-02
  2.57887930e-01  6.24772832e-02 -7.72718433e-03 -4.40183841e-03
 -7.18735112e-03  4.98322658e-02 -5.31376526e-02 -2.34771445e-01
 -2.42418777e-02  3.72860953e-02  1.16333790e-01 -1.61472969e-02]
우울 = 불안	 0.95291317
우울 = 압박	 0.5960423
공허 = 눈물	 0.76642823
행복 != 불안	 0.80137664
진정 != 우울	 0.78837603
[('기운', 0.9604686498641968), ('진이', 0.9553655982017517), ('집', 0.9546054601669312), ('불안', 0.9529131650924683), ('방', 0.9508163332939148)]
[('결과', 0.9927265048027039), ('난폭', 0.9907848834991455), ('짜증을', 0.9902779459953308), ('모든', 0.9902390241622925), ('화해', 0.9901938438415527)]
```

<div class="divider"></div>

3. Okt 인베딩 하기

```python
from gensim.models import Word2Vec
from konlpy.tag import Okt
import time

import pandas as pd 
print("1) 말뭉치 데이터 읽기 시작")
wellness_data=pd.read_excel('/content/drive/MyDrive/hackerton/wellness.xlsx')
print(len(wellness_data))
print(" 1) 말뭉치 데이터 읽기 완료: ", time.time() - start)


# 문장 단위로 명사만 추출해 학습 입력 데이터로 만듦
print(" 2) 형태소에서 명사만 추출 시작")
okt = Okt()
docs_wellness = []
for i in wellness_data['utterance(2차) '].unique():
  if not pd.isnull(i):
    docs_wellness.append(i)

docs_wellness11 = [okt.nouns(sentence) for sentence in docs_wellness]
print(" 2) 형태소에서 명사만 추출 완료:", time.time() - start)

# Word2Vec 모델 학습
print(" 3) Word2Vec 모델 학습 시작")
model_wellness = Word2Vec(sentences=docs_wellness11, size= 200, window=4, hs=1, min_count=2, sg=1)
print(" 3) Word2Vec 모델 학습 완료:", time.time() - start)

# 모델 저장
print(" 4) 모델 저장 시작")
model_wellness.save("wellness.model")
print(" 4) 모델 저장 완료:", time.time() - start)

# 학습된 말뭉치 수, 코퍼스 내 전체 단어 수
print("corpus_count :", model_wellness.corpus_count)
print("corpus_total_word : ", model_wellness.corpus_total_words)
```

모델 학습결과

```
1) 말뭉치 데이터 읽기 시작
19769
 1) 말뭉치 데이터 읽기 완료:  3241.408964395523
 2) 형태소에서 명사만 추출 시작
 2) 형태소에서 명사만 추출 완료: 3258.775744199753
 3) Word2Vec 모델 학습 시작
 3) Word2Vec 모델 학습 완료: 3260.1484937667847
 4) 모델 저장 시작
 4) 모델 저장 완료: 3261.7802832126617
corpus_count : 19672
corpus_total_word :  72453

```

Word2Vec 모델 활용

```python
from gensim.models import Word2Vec

# 모델 로딩
model_wellness = Word2Vec.load("wellness.model")
print("corpus_total_word : ", model_wellness.corpus_total_words)

# '사랑'이란 단어로 생성한 단어 임베딩 벡터
print("우울: ", model_wellness.wv['우울'])

# 단어 유사도 계산
print("우울 = 불안\t", model_wellness.wv.similarity(w1="우울", w2="불안"))
print("우울 = 압박\t", model_wellness.wv.similarity(w1="우울", w2="압박"))
print("공허 = 눈물\t", model_wellness.wv.similarity(w1="멍", w2="눈물"))
print("행복 != 불안\t", model_wellness.wv.similarity(w1="행복", w2="불안"))
print("진정 != 우울\t", model_wellness.wv.similarity(w1="진정", w2="우울"))

# 가장 유사한 단어 추출
print(model_wellness.wv.most_similar("우울", topn=5))
print(model_wellness.wv.most_similar("공허", topn=5))
```

Word2Vec 모델 활용 결과

```python
corpus_total_word :  72453
우울:  [-0.03366693  0.0508613   0.15253475  0.2527548  -0.0105314  -0.03783434
 -0.12503423  0.01425379 -0.13943464  0.18315363  0.25466534  0.1315748
 -0.25122398  0.23011918  0.05911081 -0.33841872  0.0041984   0.1444132
 -0.0313404  -0.11104241  0.20373903  0.11737736  0.13967219 -0.08333483
  0.35884157  0.08128428  0.06570961 -0.06915794  0.13901775 -0.13384718
 -0.00822338 -0.02900133  0.23395593  0.03112188  0.05395106  0.14276227
  0.1011451  -0.05569359 -0.02134604 -0.03699922 -0.03249186  0.04445758
 -0.05178045 -0.06388085 -0.09548689 -0.03121241 -0.0746647   0.02183667
  0.11441022 -0.01879629 -0.03137508 -0.0138731   0.00288217 -0.17434427
 -0.11707618 -0.15731102  0.15542862  0.04373457 -0.00751143  0.21765625
 -0.05404563  0.01274827 -0.06133746 -0.05669538  0.06225369  0.04246428
  0.23136126 -0.12000568 -0.0534712   0.0397932   0.13289908 -0.20100826
  0.03041957  0.20140874 -0.10169277 -0.02443149 -0.01810659  0.1269554
 -0.11145335  0.04098151 -0.13769099 -0.18019567 -0.05536706  0.0105897
 -0.08801583 -0.038202    0.3737911  -0.09092801 -0.04885071  0.18480639
 -0.04462237  0.08151959 -0.1621751   0.16662358  0.05005886 -0.01996391
  0.16501662  0.06744565  0.00365771 -0.20168674  0.29966772 -0.06338733
 -0.19962716  0.05694858 -0.08780891 -0.14201231 -0.22841933 -0.05324991
  0.06807344 -0.10031193 -0.27539265 -0.1688533  -0.16424452  0.3235656
  0.00471367  0.19905502 -0.02231144  0.06359375  0.29702067  0.09528488
  0.13046655  0.03059065 -0.07966805  0.12752116  0.10455493 -0.30158916
 -0.17855583 -0.27453214 -0.23402688 -0.1132561  -0.05214899 -0.19108212
 -0.04783627  0.01863869 -0.0608252   0.09148327  0.03781789 -0.09513913
  0.07850092 -0.19816908 -0.00745267 -0.19817452  0.05103672  0.16211605
  0.21428709  0.1544065   0.00561004  0.10689791 -0.13168833  0.09226021
 -0.16955489 -0.352273   -0.12847246 -0.3077868   0.09171231  0.07432263
 -0.21008508 -0.09978942  0.04221807 -0.00142549  0.12326061 -0.14924188
  0.11640368  0.05128044 -0.22481722 -0.1965679   0.4249643   0.10813201
 -0.00365569 -0.14142293  0.232573   -0.03175408  0.22495015  0.1786142
 -0.05598661 -0.07219592  0.03647596 -0.11767389 -0.01535862  0.14173609
  0.1757104  -0.13437118 -0.09608817  0.02257651 -0.11267725 -0.09759824
  0.06841267 -0.03139738 -0.24492362 -0.03876304 -0.13031848  0.09603998
  0.11594737 -0.01755376  0.00181734 -0.3203166  -0.07482132  0.02887551
  0.082184   -0.16158202]
우울 = 불안	 0.7495002
우울 = 압박	 0.9481326
공허 = 눈물	 0.7807349
행복 != 불안	 0.88688415
진정 != 우울	 0.42998204
[('순산', 0.9620715379714966), ('탈', 0.9512975215911865), ('압박', 0.9481325149536133), ('구역', 0.9362142086029053), ('거부', 0.9239566922187805)]
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-78-82b85390a46b> in <module>
     17 # 가장 유사한 단어 추출
     18 print(model_wellness.wv.most_similar("우울", topn=5))
---> 19 print(model_wellness.wv.most_similar("침울", topn=5))

1 frames
/usr/local/lib/python3.7/dist-packages/gensim/models/keyedvectors.py in word_vec(self, word, use_norm)
    450             return result
    451         else:
--> 452             raise KeyError("word '%s' not in vocabulary" % word)
    453 
    454     def get_vector(self, word):

KeyError: "word '침울' not in vocabulary"
```

* okt는 띄어쓰기 기반이라 단어가 '형용사, 부사'가 되면 인식을 못한다. ex) 위에 침울이라는 단어를 못 찾는 모습

* ## >> kkma은 생각보다 (심리상담) 정서적인 측면에서 잘 맞는 듯