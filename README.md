### 2020 서울 하드웨어 해커톤 sim_tact 팀

나만의 쇼핑 광고판 Mynage
=============
언택트 시대에 필요한 기술로 저희는 Mynage(마이니지)를 제안합니다. 마이니지는 My와 Signage의 합성어로, 카트에 부착하여 사용하는 위치 기반의 판촉 시스템입니다.  
&nbsp;
&nbsp;
>  &nbsp;지금까지 오프라인 매장에서 제공해왔던 판촉의 행위로는 시식, 시착, 시연 등 대면 기반의 판촉이 주류를 이뤘습니다. 그러나 특히 시식을 통한 판촉이나 직접 말로 제품을 홍보하는 판촉 행위는 언택트 시대에 적합하지 않은 판촉 방법이며, 이제 언택트 시대에 알맞은 판촉 방법이 필요할 때입니다. 
>
>  &nbsp;본 프로젝트에서 제안하는 마이니지는 디지털 판촉방식을 제공함으로써 오프라인 매장에서 인력을 최소화하는 동시에 효과적인 판촉을 할 수 있는 쇼핑 카트 부착형 시스템입니다. 마이니지는 기존에 시행되던 대면 기반의 판촉 행위를 비대면으로 전환할 수 있도록 도우며, 매장 내 위치를 기반으로 고객에게 적합한 판촉 정보를 제공하는 시스템입니다. 이를 통해 고객은 자신에게 필요한 정보를 제공받을 수 있고, 기업은 판매 대상에게 선택적으로 상품 광고를 할 수 있으며, 매장에서는  위치정보를 활용하여 매대 진열의 효율을 높일 수 있을 것입니다.

&nbsp;
&nbsp;
## 팀원소개
* 임효주(팀장) : 프로젝트 기획, SW 디버깅, 3D print 모델링
* 박영건 : SW개발 
* 최현경 : HW개발
* 박민아 : HW 디버깅, 아두이노(비콘) 

&nbsp;
&nbsp;
## 프로젝트 목적 
&nbsp; 
코로나 언택트 시대를 살고있음에도 아직 마트의 판촉 시스템은 사람이 직접 컨택하는 형태를 띄고 있습니다. 또한 판촉상품이 아닌 물건들에 대해서는 직접 찾아보지 않는이상 구매가 쉽지 않습니다. 우리는 지하철에서도 쉽게 볼 수 있는 디지털 광고판인 사이니지에서 영감을 얻어 카트에 탈부착 가능한 디지털 사이니지 시스템을 기획하게 되었습니다. 이는 무작위 추천이 아닌 위치센서(비콘)를 기반으로 현재 위치에서 판매하는 물품을 추천할 수 있는 시스템입니다.
&nbsp;
&nbsp;
## 파일 리스트

&nbsp;
&nbsp;
## 보드
* RPI4 : 비콘 신호 수신 및 위치계산, 상품정보... 
* 아두이노 우노 : 비콘 업로드 (github.com/thebirds0324/sim_tact/blob/master/beacon_upload.ino)
&nbsp;
&nbsp;

## 기능

<p align="center">
<img width="914" alt="스크린샷 2020-09-04 오후 7 20 41" src="https://user-images.githubusercontent.com/49704910/92229001-c0ed8580-eee3-11ea-8212-0b86742a8baa.png">
  </p>

<h5 align="center">Front-end 구상도</h5>
  
디스플레이상에서 현재 위치, 해당 위치에서 판매되는 추천 물품 리스트를 확인할 수 있다. 또한 특정 물건 검색 기능을 사용할 수 있다.
&nbsp;
&nbsp;

(2) 기능
위치 기반의 물품 추천 시스템
수신되는 신호를 기반으로 현재 위치에서 판매하는 물품에 대해 추천해주는 시스템. 실내 측위를 위해 특정 위치마다 비콘 발신기를 설치한다. 한 위치를 특정하기 위한 비콘의 갯수는 최소 4개이다. 현재 위치에서 수신되는 신호를  기반으로 현재 위치를 특정한다. 

[ 위치 특정 알고리즘 ]

<p align="center">
<img width="278" alt="스크린샷 2020-08-28 오후 8 07 05" src="https://user-images.githubusercontent.com/49704910/91554468-254f9880-e96a-11ea-84c6-75215ab61499.png">
  </p>
  
위치 A,B,C,D에 해당하는 비콘값은 A={1,2,3,4} B={2,3,5,6} C= {4,5,7,8} D={5,6,8,9}이다. 
1) 사용하는 device name으로 필터링
2) 2m이내의 신호값만 받도록 필터링 
3) 가장 거리 가까운 송신기를 Key값으로 두고,  해당 Key값이 포함되는 영역과 수신된 신호 비콘신호값들 유사도 확인
4) 가장 높은 유사도를 갖는 영역을 현재 영역으로 판단.  (단, 75%미만일 경우나 다른 예외상황에서는 갱신하지 않음) 
5) 5초 단위 싸이클로 반복

&nbsp;
&nbsp;


