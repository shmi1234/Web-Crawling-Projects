<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<header>
  <h1>부동산 데이터 수집 웹크롤링 프로젝트</h1>
</header>

<nav>
  <ul>
    <li><a href="#section1">프로젝트 개요</a></li>
    <li><a href="#section2">팀원 소개</a></li>
    <li><a href="#section3">프로젝트 설치 및 실행 방법</a></li>
    <li><a href="#section4">프로젝트 목표 및 설계</a></li>
    <li><a href="#section5">프로젝트 결론</a></li>
  </ul>
</nav>

<main>
  <section id="section1">
    <h2>프로젝트 개요</h2>
    <p>
        최근 수행된 설문 조사에 따르면, 20대의 1,094명을 대상으로 한 조사 결과에 따르면, 20대의 주요 목표로는 내 집을 마련하는 것이 큰 비중을 차지합니다. 주식이나 코인을 포함한 재테크(20%), 대출 상환(27%), 여행(38%), 저축(52%) 등이 있지만, 내 집 마련이 75%의 응답자가 선택한 답안으로 나타났습니다...
    </p>
  </section>
  
  <section id="section2">
    <h2>팀원 소개</h2>
     <ul>
      <li>윤상하(조장) : 기획, PPT</li>
      <li>박성훈 : 기획, 제안, 기능 개발</li>
      <li>정선우 : 기획</li>
      <li>김동규 : 기획, 제안</li>
    </ul>
  </section>

<section id="section3">
  <h2>프로젝트 설치 및 실행 방법</h2>
  <ul>
    <li><a href="Project01.ipynb">Project01.ipynb</a> - 데이터 수집을 위해서 만든 코드 입니다.</li>
    <li><a href="Project Pandas.ipynb">Project Pandas.ipynb</a> - 데이터 수집 이후 시각화 자료를 만든 것 입니다.</li>
    <li><a href="서울시 아파트 상한가.xlsx">서울시 아파트 상한가.xlsx</a> - 수집한 데이터를 엑셀화 시켜서 정리해놓은 엑셀 파일 입니다.</li>
    <li><a href="https://github.com/shmi1234/Web-Crawling-Projects/tree/main/PPT%20%EB%B6%84%ED%95%A0%EC%95%95%EC%B6%95">PPT 분할압축<a>
      - PPT의 용량이 커서 PPT 분할압축 파일을 넣어둔 폴더 입니다.</li>
  </ul>
</section>

<section id="section4">
  <h2>프로젝트 목표 및 설계</h2>
  <h4>[데이터 수집]</h4>
  <p>
    아실 <a href="https://asil.kr/">https://asil.kr/</a> 네이버 부동산 <a href="https://new.land.naver.com/">https://new.land.naver.com/</a>
    서울시를 대상으로 25개구에 위치한 467개 동에 대해 총 3,846개의 아파트 별 실 거래가를 수집 하였습니다. 이를 통해 각 아파트의 실 거래가 정보를 상세히 파악할 수 있으며, 서울시 내의 다양한 지역에서 발생하는 부동산 시장의 동향을 분석할 수 있습니다.
  </p>
  <h4>[아실 사이트의 Iframe]</h4>
  <p>
    Inline Frame(iframe)은 웹 페이지 안에 또 다른 웹 페이지를 삽입하는 기능을 의미합니다. 현재 브라우저에서 렌더링 되는 문서 안에 다른 HTML 페이지를 삽입하여 표시할 수 있도록 합니다. 그러나 최근에는 보안 문제, 모바일 호환성 및 대체 명령어 등장 등의 이유로 사용이 줄어 들고 있는 추세입니다.
  </p>
  <p>
    XPath가 /html/body/div[2]/div[1]/div[1]/div[3]/a[1]인 경우 브라우저가 탐색 실패 오류를 반환할 때, 이는 해당 소스가 id가 'sub1'인 iframe 안에 존재하기 때문입니다. 이를 해결하기 위해서는 먼저 해당 iframe으로 진입해야 합니다. 이를 위해 진입할 iframe을 변수로 지정하고, Browser.switch_to.frame() 메서드를 사용하여 해당 iframe으로 진입합니다. 데이터를 추출한 후에는 Browser.switch_to.default_content() 메서드를 사용하여 상위 HTML로 돌아갑니다. 이 작업을 수행해야 다른 iframe에 있는 데이터를 추출할 수 있습니다.
  </p>
  <p>
    테이블의 각 row에서 데이터를 추출하기 위해 for 루프를 사용하는데, 해당 코드가 Selenium이 데이터를 한 번만 추출한 후에는 이후의 for 루프에서 경로를 찾지 못하고 오류가 발생하는 문제가 있습니다. 이를 해결하기 위해서는 데이터를 추출할 때마다 iframe으로 진입하여 작업을 수행해야 합니다. 테이블의 전체 텍스트를 불러올 수 있지만 줄바꿈 삽입으로 데이터를 가공하는 것이 어려울 수 있습니다.
  </p>
  <h4>[네이버 부동산 사이트]</h4>
  <p>
    브라우저 진입 및 데이터 웹 크롤링을 위한 사이트 링크 파도타기를 진행하고, 서울시의 모든 '구'를 리스트화 하여 추가합니다. 그 후 각 '구'에 포함된 '동' 리스트도 생성하고, 각 '동'에 포함된 모든 '아파트' 리스트를 만듭니다. 데이터를 웹 크롤링 하는 과정에서 '평수'와 '매물' 정보가 없는 경우에는 오류가 발생할 수 있습니다. 이를 해결하기 위해 try ~ except 구문을 활용하여 예외 처리를 수행하였습니다. 각 아파트의 평수를 구분하기 위해 리스트 처리를 하고, 각 아파트를 해당 평수 별로 분류한 후 '상한가' 데이터를 찾습니다. 마지막으로, CSV 파일에 입력을 위해 결과값이 나오는 데이터를 추가할 final_list를 만들고, 각 구에 대한 동 별로 데이터를 정리합니다. 면적 별로 '상한가' 데이터를 입력 받고, 해당 매물이 없는 경우에는 'None' 데이터를 삽입하여 구분합니다. 최종적으로 약 2000개의 상한가 데이터를 CSV 파일로 정렬하여 출력합니다. 
  </p>
  <h4>[시각화]</h4>
  <p>
    자치구별로 아파트의 수를 비교하고, 각 자치구에서의 최고가와 최저가를 비교해보며, 마지막으로 자치구별로 평균가를 비교하고자 합니다. 먼저, 서울시의 각 자치구에서 아파트의 수를 측정하고 비교합니다. 그런 다음, 각 자치구에서의 아파트 중에서 최고가와 최저가를 확인하여 비교합니다. 마지막으로, 각 자치구에서의 아파트의 평균가를 계산하여 비교합니다. 이러한 분석을 통해 서울시의 각 자치구가 아파트 시장에서 어떻게 위치하고 있는지를 이해할 수 있습니다.
  </p>
</section>

<section id="section5">
  <h2>프로젝트 결론</h2>
  <p>
    이 데이터 수집과 시각화를 통해 우리는 서울시 부동산 시장의 현황을 더 잘 이해할 수 있게 되었습니다. 먼저, 아실과 네이버 부동산 사이트를 통해 수집한 정보를 통해 서울시 25개구에 위치한 467개 동에 총 3,846개의 아파트에 대한 실 거래가를 상세히 파악할 수 있었습니다. 이를 통해 서울시 내 다양한 지역에서 발생하는 부동산 시장의 동향을 분석할 수 있었습니다.

특히, 아실 사이트의 iframe을 통해 데이터를 수집하는 과정에서 Selenium을 사용하면서 발생한 문제들을 해결하는 과정은 새로운 도전이었습니다. 또한, 네이버 부동산 사이트에서도 데이터를 웹 크롤링 하는 과정에서 예외 처리를 통해 문제를 극복하는 등 다양한 어려움을 만났지만, 이를 해결하고 데이터를 성공적으로 수집할 수 있었습니다.

시각화를 통해 자치구별로 아파트의 수, 최고가, 최저가, 그리고 평균가를 비교함으로써, 서울시 각 자치구의 부동산 시장에서의 위치와 특징을 파악할 수 있었습니다. 이러한 분석을 통해 부동산 투자나 거주지 선정 등의 의사 결정에 도움을 줄 수 있을 것으로 기대됩니다.

팀별 단위로 진행한 첫 프로젝트였습니다. 처음에는 Iframe과 같이 웹 크롤링하기 어려운 과제에 직면했지만, 결국 데이터 수집에는 성공했습니다. 그러나 데이터 가공에 어려움을 겪게 되었고, 팀원들과 의견을 조율한 끝에 네이버 부동산 사이트로 다시 웹 크롤링을 시작하게 되었습니다. 이후에는 프로젝트를 성공적으로 완료하여, 팀원들과의 신뢰를 쌓고 서로 돈독한 관계를 형성하게 되었습니다.
  </p>
</section>

</main>

<footer>
  <p>&copy; 2024 부동산 데이터 수집 웹크롤링 프로젝트</p>
</footer>

</body>
</html>
