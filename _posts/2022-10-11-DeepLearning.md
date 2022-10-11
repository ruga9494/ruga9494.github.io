---
title: 딥러닝/인공지능 - 선형회귀
updated: 2022-10-11 22:54
---

### 학습영상

url : https://www.youtube.com/watch?time_continue=80&v=PYTZ65FzEG4&feature=emb_title&ab_channel=%EB%B0%95%ED%95%B4%EC%84%A0 <br>
url : https://www.youtube.com/watch?v=VVArHrsxrYU&ab_channel=%EB%B9%B5%ED%98%95%EC%9D%98%EA%B0%9C%EB%B0%9C%EB%8F%84%EC%83%81%EA%B5%AD

<div class="divider"></div>

선형 회귀는 기울기와 절편을 찾아준다.


### AI 챗봇 

```python
import streamlit as st 
from streamlit_chat import message
import pandas as pd
from sentence_transformers import SentenceTransformer
from sklearn.metrics.pairwise import cosine_similarity
import json

# 로드를 한번만 한 후에 캐쉬에 저장
@st.cache(allow_output_mutation=True)
def cached_model():
    model = SentenceTransformer('jhgan/ko-sroberta-multitask')
    return model

#인베딩
@st.cache(allow_output_mutation=True)
def get_dataset():
    df = pd.read_csv('wellness_dataset.csv')
    df['embedding'] = df['embedding'].apply(json.loads)
    return df

# 모델 불러오기
model = cached_model()
# 데이터셋 불러오기
df = get_dataset()

st.header('심리상담 챗봇')

if 'generated' not in st.session_state:
    # 챗봇이 대화한 내용을 저장
    st.session_state['generated'] = []

if 'past' not in st.session_state:
    # 사용자가 대화한 내용을 저장 / 나갔다와도 초기화 되지 않는 점을 방지
    st.session_state['past'] = []

# 챗봇 대화메세지 작성, 보내기 버튼
with st.form('form', clear_on_submit=True): # 전송 후 Textbox 초기화
    user_input = st.text_input('당신: ', '') # 사용자 대화 입력
    submitted = st.form_submit_button('전송') # 전송버튼

if submitted and user_input:
    embedding = model.encode(user_input) # 대화 한 것을 (벡터)인코딩

    df['distance'] = df['embedding'].map(lambda x: cosine_similarity([embedding], [x]).squeeze())# 사용자가 입력한 문장과 데이터셋을 비교해줌
    answer = df.loc[df['distance'].idxmax()] # 비교 후 최대값을 도출

    st.session_state.past.append(user_input) # 사용자 대화 past에 저장
    st.session_state.generated.append(answer['챗봇']) # 챗봇의 답변을 generated에 저장

# 사용자 대화와 챗봇의 결과를 메세지로 표시해주는 단계
for i in range(len(st.session_state['past'])):
    message(st.session_state['past'][i], is_user=True, key=str(i) + '_user')
    if len(st.session_state['generated']) > i:
        message(st.session_state['generated'][i], key=str(i) + '_bot')

```