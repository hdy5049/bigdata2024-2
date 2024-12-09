# bigdata2024-2
빅데이터 기초 2학기 

!pip install koreanize-matplotlib

import koreanize_matplotlib


# 필요한 라이브러리 불러오기
import pandas as pd

# 파일들을 읽어오기
df1 = pd.read_excel('/content/drive/MyDrive/Colab Notebooks/국적_지역__및_체류자격별_외국인_입국자_2023.xlsx')
df2 = pd.read_excel('/content/drive/MyDrive/Colab Notebooks/국적_지역__및_체류자격별_체류외국인_현황_2020.xlsx')
df3 = pd.read_excel('/content/drive/MyDrive/Colab Notebooks/국적_지역__및_체류자격별_체류외국인_현황_2021.xlsx')
df4 = pd.read_excel('/content/drive/MyDrive/Colab Notebooks/국적_지역__및_체류자격별_체류외국인_현황_2022.xlsx')

# 데이터프레임의 정보 확인
print("df1 데이터프레임 미리보기")
print(df1.head(), "\n")

print("df2 데이터프레임 미리보기")
print(df2.head(), "\n")

print("df3 데이터프레임 미리보기")
print(df3.head(), "\n")

print("df4 데이터프레임 미리보기")
print(df4.head(), "\n")
-------------------------------------------------------
import matplotlib.pyplot as plt

# 연령대 및 남성/여성 데이터 (예시 데이터)
age_groups = ['0-9', '10-19', '20-29', '30-39', '40-49', '50-59', '60-69', '70-79', '80+']
male_population = [-1000, -1200, -1500, -1700, -1600, -1400, -1200, -800, -500]  # df에서 가져올 실제 데이터
female_population = [1100, 1300, 1600, 1800, 1700, 1500, 1300, 900, 600]  # df에서 가져올 실제 데이터

# 그래프 생성
plt.barh(age_groups, male_population, color='blue', label='남성')
plt.barh(age_groups, female_population, color='pink', label='여성')

# 그래프 설정
plt.title('2023년 인구 피라미드')
plt.xlabel('인구수')
plt.ylabel('연령대')
plt.legend()
plt.grid(axis='x')

plt.show()
-------------------------------------------------------------------------------------
# 체류 자격별 데이터 (예시: 2022년 데이터)
categories = [
    'A1(외교)', 'A2(공무)', 'B1(사증면제)', 'B2(관광통과)', 'C1(일시취재)', 'C3(단기방문)', 'C4(단기취업)',
    'F2(거주)', 'F3(동반)', 'F4(재외동포)', 'F5(영주)', 'F6(결혼이민)', 'G1(기타)', 'H1(관광취업)',
    'H2(방문취업)', 'T1(관광상륙)', '승무원'
]
values = [
    5695, 4149, 224817, 100793, 20, 137642, 1985, 44561, 24917, 502451, 176107,
    136266, 36446, 2337, 105567, 216, 756016
]  # df에서 가져올 실제 데이터

# x축 위치 정의
x_positions = range(len(categories))

# 그래프 생성
plt.figure(figsize=(12, 6))
plt.bar(x_positions, values, color='green')

# x축 레이블 설정
plt.xticks(x_positions, categories, rotation=45, ha='right')  # 카테고리 표시

# 그래프 설정
plt.title('2022년 체류 자격별 외국인 수')
plt.xlabel('체류 자격')
plt.ylabel('인원 수')

plt.show()
----------------------------------------------------------------------------------------------------
# 체류 자격별 비율 데이터 (예시: 2021년 데이터)
labels = [
    'A1(외교)', 'A2(공무)', 'B1(사증면제)', 'B2(관광통과)', 'C1(일시취재)', 'C3(단기방문)', 'C4(단기취업)',
    'F2(거주)', 'F3(동반)', 'F4(재외동포)', 'F5(영주)', 'F6(결혼이민)', 'G1(기타)', 'H1(관광취업)',
    'H2(방문취업)', 'T1(관광상륙)', '승무원'
]
sizes = [
    5179, 3815, 165869, 43673, 18, 97225, 1691, 42367, 21237, 478442, 168118,
    134285, 30158, 327, 125493, 235, 77472
]  # df에서 가져올 실제 데이터
colors = [
    'gold', 'lightblue', 'lightgreen', 'pink', 'purple', 'orange', 'cyan', 'red',
    'blue', 'green', 'yellow', 'magenta', 'gray', 'brown', 'lime', 'navy', 'olive'
]

# 원형 차트 생성
plt.figure(figsize=(10, 10))
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90, colors=colors)

# 그래프 설정
plt.title('2021년 체류 자격별 비율')

plt.show()
-------------------------------------------------------------------------------
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker  # y축 숫자 형식 지정용 라이브러리
import pandas as pd

# 필요한 열과 연도 데이터 추출
columns_to_extract_2023 = ['국적(지역)별(1)', '2023']
columns_to_extract_2022 = ['국적(지역)별(1)', '2022']
columns_to_extract_2021 = ['국적(지역)별(1)', '2021']
columns_to_extract_2020 = ['국적(지역)별(1)', '2020']

# 각 연도 데이터 선택
df_2023 = df1[columns_to_extract_2023].dropna()
df_2022 = df4[columns_to_extract_2022].dropna()
df_2021 = df3[columns_to_extract_2021].dropna()
df_2020 = df2[columns_to_extract_2020].dropna()

# 각 데이터프레임을 하나로 병합
df_combined = pd.merge(df_2020, df_2021, on='국적(지역)별(1)', how='outer')
df_combined = pd.merge(df_combined, df_2022, on='국적(지역)별(1)', how='outer')
df_combined = pd.merge(df_combined, df_2023, on='국적(지역)별(1)', how='outer')

# 인덱스 설정
df_combined.set_index('국적(지역)별(1)', inplace=True)
df_transposed = df_combined.T  # 전치하여 연도를 인덱스로 변환

# 꺾은선 그래프 생성
plt.figure(figsize=(12, 6))
for country in df_transposed.columns:
    plt.plot(df_transposed.index, df_transposed[country], marker='o', label=country)

# 그래프 설정
plt.title('2020-2023년 국적별 외국인 현황', fontsize=16)
plt.xlabel('년도', fontsize=12)
plt.ylabel('인구 수', fontsize=12)

# y축 범위 및 숫자 표시 설정
plt.ylim(0, 5000000)  # y축 범위 설정
ax = plt.gca()
ax.yaxis.set_major_locator(ticker.MultipleLocator(300000))  # y축 주요 눈금을 100,000 단위로 설정
ax.yaxis.set_minor_locator(ticker.MultipleLocator(100000))  # y축 보조 눈금을 50,000 단위로 설정
ax.yaxis.set_major_formatter(ticker.FuncFormatter(lambda x, pos: f'{int(x):,}'))  # 천 단위 콤마 추가

plt.legend(title='국적', fontsize=10, loc='upper left')
plt.grid(True)

# 그래프 표시
plt.show()
