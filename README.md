Logstash install with ansible

Hey! I’m your first Markdown document in StackEdit1. Don’t delete me, I’m very helpful! I can be recovered anyway in the Utils tab of the  Settings dialog.

기본 구조

Directories schema

Logstash install with ansible 프로젝트는 아래와 같은 스키마로 구성되어 있습니다 :

Information

프로젝트 이름은 ansible-km-iris-logstash 입니다.
ansible 버전은 2.3입니다.
클러스터 구조에 적합하게 설정되도록 스키마가 정의되어 있지만 Single Machine에도 설치 될 수 있도록 구조화 되어 있습니다.
Directory	Desc
group_vars	Logstash를 설치하기 위한 전역 설정 값들이 정의되어 있습니다.
inventories	설치할 서버의 정보가 정의되어 있습니다.
roels	Logstash 기본적인 설치 및 사전에 설정되어야 하는 태스크들이 정의 되어 있습니다.
