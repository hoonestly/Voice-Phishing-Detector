# Korean Voice Phishing Detector - (DOCTOR PHISH)

This repository demonstrates our exploration of Korean voice phishing detection, utilizing two distinct methodologies for enhanced accuracy and reliability. Initially developed using LSTM Model to harness their sequential data processing capabilities, our model achieved a foundational level of success in identifying voice phishing attempts. Recognizing the opportunity for enhancement, we transitioned to leveraging KoBERT, a model pre-trained on the Korean language. This strategic update significantly improved our system's ability to understand the complexities and nuances of Korean speech, offering a more accurate and reliable solution for detecting voice phishing scams.

## 👪 Teammates
- Team name: **Doctor Phish**
- **Jeonghoon Ko**: Yonsei University, major in Sociology, leader of team Dr. Phish
- **Youngjin Son**: Korea University, major in Business, PM 
- **Yunjeong Lee**: Korea University, major in Art and Design, UX/UI designer 
- **Hyeongjun Kim**: Yonsei University, major in artificial intelligence, Developer

## 📋 Datasets
- stopword.txt: 
    - Preprocessed to remove stop words - https://www.ranks.nl/stopwords/korean
- combined_dataset.csv
    - Boussougou, M. K. moussavou. (2022). Korean Call Content Vishing (KorCCVi) Dataset. Korean_Voice_Phishing_Detection. https://github.com/selfcontrol7/Korean_Voice_Phishing_Detection
    - 민원(콜센터) 질의-응답 데이터 (금융/보험). (2023). AI Hub. https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=98
    - 일상 대화 말뭉치 2022. (2022). 문화체육관광부 국립국어원 언어정보나눔 모두의 말뭉치. https://kli.korean.go.kr/corpus/main/requestMain.do?lang=ko

## 🖥 Model
### A. LSTM model

-**Dataset used**: combined_data.csv <br>
-**Train**:Test ratio set to 0.8:0.2 <br>
-**Epochs** of 5, **learning rate** of 1e -1, **batch size** of 32, **max_len** = 512 <br>
-**Performance metrics  at train   at test** <br>
    accuracy          0.9892      0.9892  <br>
    loss              0.0312      0.0228  <br>
**Precision**: 0.9702, **Recall**: 0.9267, **F1 Score**: 0.9480

### B. A KoBERT based detection model

-**Dataset used**: combined_data.csv <br>
-**Train**:Validation ratio set to 0.8:0.2 <br>
-**Epochs** of 2, **learning rate** of 1e -5, **batch size** of 32, **max_len** = 512 <br>
-**Performance metrics  at train   at validation** <br>
    accuracy          0.9955      0.9961  <br>
    loss              0.9892      1.0000  <br>

## 🔖 Result
### **Combined_dataset.csv - KoBERT**
``여보세요 네 안녕하세요 서울중앙지방검찰청 00부 담당 형사 000입니다. 000님 맞으십니까? 맞는데요 다름이 아니고 혹시 김00님을 아십니까? 지금 김00님이 경남은행에서 000님 명의로 대포통장을 개설하였습니다....``
- 보이스피싱 : 0.99976

``안녕하세요, 어떻게 도와드릴까요? 안녕하세요, 최근에 업무 스트레스 때문에 정말 힘들어요. 네, 이해해요. 어떤 일이 스트레스를 유발하고 있나요? 업무 부하가 매우 많고, 기간 내에 모든 것을 해내기 어려워서...``
- 일반대화 : 0.99995

``안녕하세요, 은행에 오신 것을 환영합니다. 어떤 서비스를 도와드릴까요? 안녕하세요, 저는 새로운 계좌를 개설하고 싶은데요, 어떤 서류가 필요한가요 신분증과 주민등록등본, 그리고 초기 입금할 현금이나 체크카드가...``
- 일반대화 : 0.99995

``안녕하세요, 경찰서입니다. 어떻게 도와드릴까요? 안녕하세요, 제가 지금 길을 걷고 있는데요, 이상한 사람이 계속 따라오는 것 같아요. 알겠습니다. 현재 위치와 그 사람의 특징을 자세히 설명해주시...``
- 일반대화 : 0.99978

## 💡 Further Work
Using the OpenAI API with the GPT-3.5-turbo model, we have developed a feature that categorizes the type of voice-phishing if detected. If the text is classified as voice-phishing with a confidence level of 0.95 or higher, the system will categorize the type of voice-phishing and display a warning message

``여보세요 네 안녕하세요 서울중앙지방검찰청 00부 담당 형사 000입니다. 000님 맞으십니까? 맞는데요 다름이 아니고 혹시 김00님을 아십니까? 지금 김00님이 경남은행에서 000님 명의로 대포통장을 개설하였습니다....``
- 보이스피싱 : 0.99976 
```
### 보이스피싱 유형: 사칭 조사관을 사칭한 사례

**상황 분석:**
- 전화를 받은 상대방이 검찰청 조사관이라고 주장하며 피해자나 용의자인지 확인하기 위해 전화를 걸어왔다고 주장합니다.
- 대포통장을 개설하여 범죄에 연루된 것이 있는지 확인하기 위해 본인 확인과 진술을 요구합니다.

**대응 방안:**
1. 즉시 통화를 종료하고 해당 기관의 공식 연락처로 직접 연락하여 상황을 확인합니다.
2. 개인 정보나 금융 정보를 절대 제공하지 않습니다.
3. 보이스피싱 의심 통화는 지역 경찰청이나 금융감독원에 신고합니다.

💡 **권고 사항:** 반드시 지역 경찰청이나 검찰청의 공식 연락처로 직접 확인 후, 보이스피싱 사례임을 신고하는 것이 중요합니다. 위와 같은 사칭 조사관에게는 개인 정보를 누설하지 않도록 주의해야 합니다.
```

## References
[1] 안상준, & 유원준 . (2022, November 14). 10-08 BiLSTM으로 한국어 스팀 리뷰 감성 분류하기. 딥 러닝을 이용한 자연어 처리 입문. https://wikidocs.net/94748 <br>
[2] M. K. M. Boussougou, S. Jin, D. Chang, and D.-J. Park, “Korean Voice Phishing Text Classification Performance Analysis Using Machine Learning Techniques,” Proceedings of the Korea Information Processing Society Conference, pp. 297–299, Nov. 2021. <br>
[3] M. K. M. Boussougou and D.-J. Park, “A Real-time Efficient Detection Technique of Voice Phishing with AI,” Proceedings of the Korean Institute of Information Scientists and Engineers Korea Computer Congress; Korean Institute of Information Scientists: Jeju, Republic of Korea, vol. 11, no. 10, pp. 768–770, June. 2021. <br>
[4] M전동흔, “'보이스피싱' 줄었지만...건당 피해액은 증가”, YTN, 2024.02.25, https://www.youtube.com/watch?v=VXfGFU8jvCE