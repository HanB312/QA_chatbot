# 📘 논문 기반 QA Chatbot (Document-based QA System)

**QA Chatbot**은 업로드된 PDF 문서를 기반으로 사용자의 질문에 답변하는  
문서 기반 질의응답(QA, Question Answering) 시스템입니다.  

이 프로젝트는 **LangChain + Hugging Face**를 활용하여,  
문서를 벡터 임베딩한 후 관련 문맥을 검색(Retrieval)하고  
TinyLlama 모델을 통해 답변을 생성합니다.


> 참고 논문  
> “DAEM-ERC: 대화에서의 감정 인식을 위한 데이터 증강과 앙상블 기반 모델,” 한국정보과학회, 2023.

---

## 프로젝트 개요

| 항목 | 내용 |
|------|------|
| 프로젝트명 | QA Chatbot |
| 주요 기술 | `Python`, `LangChain`, `Hugging Face`, `FAISS`, `TinyLlama` |
| 모델 | `TinyLlama/TinyLlama-1.1B-Chat-v1.0` |
| 데이터 | 사용자가 업로드한 PDF 문서 |
| 목표 | 문서 내용을 기반으로 질의응답 수행 |

---

## 주요 기능

1. **PDF 문서 로드 및 분할**
   - LangChain의 `PyPDFLoader`와 `RecursiveCharacterTextSplitter` 사용  
   - 문서 내용을 작은 청크로 분할하여 임베딩 효율화

2. **임베딩 & 벡터 검색**
   - `sentence-transformers/all-MiniLM-L6-v2` 임베딩 모델 활용  
   - `FAISS`로 빠르고 효율적인 유사 문서 검색 수행

3. **LLM을 통한 답변 생성**
   - `TinyLlama-1.1B-Chat-v1.0`으로 문맥 기반 답변 생성  

4. **RAG (Retrieval-Augmented Generation) 구조**
   - 문서 검색 결과를 LLM에 전달하여 근거 기반 답변 생성

---

## 시스템 구성도
📄 PDF 문서  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓  
[Text Splitter] → [Embedding Model] → [FAISS Vector Store]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓  
[LLM (TinyLlama)]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓  
💬 최종 답변 생성  

---

## 실행 방법

### 1. 필수 라이브러리 설치
```bash
pip install -U torch transformers langchain langchain-community sentence-transformers faiss-cpu pypdf
```

### 2. chat.ipynb 실행

(1) PDF 파일을 업로드하고 셀을 순서대로 실행합니다.

(2) ask("질문 내용") 함수를 통해 질의응답을 수행합니다.



---


## 한계점
| 항목              | 설명                               |
| --------------- | -------------------------------- |
| TinyLlama 모델 한계 | 영어 중심 학습으로 한국어 이해력이 낮음           |
| 긴 문맥 처리 한계      | 입력 토큰 제한(2048)으로 긴 문서 요약 시 정보 손실 |
| QA 불안정성         | 프롬프트를 그대로 반복하거나 답변을 생략하는 경우 발생   |



---
## 향후 보완 계획
1. **요약형 RAG 추가**
   - 긴 문서를 요약 후 질의응답하는 “2단계 RAG 구조” 도입
   - 토큰 한계 문제 해결

2. **UI 인터페이스 구축**
   - Streamlit 기반 간단한 웹 UI 추가 예정
   - 문서 업로드 → 질문 입력 → 답변 확인 흐름 지원
---
