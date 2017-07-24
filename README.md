ansible-km-iris-logstash
=======================

[![logstash](https://img.shields.io/badge/Logstash-5.5.0-brightgreen.svg)](https://www.elastic.co/guide/en/logstash/current/introduction.html)
[![ansible](https://img.shields.io/badge/ansible-2.3-orange.svg)](https://www.ansible.com/it-automation)

##### Ansible을 이용하여 Elastic stack의 일부인 Logstash 5.5.0을 다수의 서버에 설치할 수 있습니다. #####   

_Directories schema_

Directory | desc  |
| ------------- | ------------- |
| group_vars | `Logstash`를 install하기 위한 전역 설정 값들이 정의되어 있습니다. |
| inventories  | 설치할 서버 정보가 정의되어 있습니다.  |
| roles  | 디렉터리 생성, JDK 설정 등과 같은 기본 설정과 `Logstash` 설치까지의 모든 과정이 태스크로 정의되어 있습니다. |`

_**사용전 변경할 설정 항목들 확인**_
> 디렉터리 : group_vars  
> 파일이름 : all  

items | desc  | 필수 확인 항목
| ------------- | ------------- |---|
| account.user | 실행 계정의 아이디  |Y
| account.group  | 실행 계정의 그룹  |Y

_**Logstash input config 관련 항목들 확인**_
> 디렉터리 : group_vars  
> 파일이름 : all  

items | desc  | 필수 확인 항목
| ------------- | ------------- |---|
| logstash.conf.input.bootstrap_servers | Kafka 주소를 참고하여 쉼표를 구분으로 설정  |Y
| logstash.conf.input.codec  | 코덱으로 사용할 종류  |Y

###   (디렉터리 : group_vars , 파일이름 : all)
> **Logstash input config**
> 
> - **logstash.conf.input.bootstrap_servers** 
> - **** 
> - **logstash.conf.input.group_id** Kafka에서 가져올 메시지에 대한 그룹 아이디 (단일 서버 및 다른 클러스터일 경우엔 그룹 아이디를 다르게 적용)
> - **logstash.conf.input.client_id** 해당 프로젝트를 구분하는 네이밍으로 적당히 설정

### Logstash input config 관련 항목들 확인 (디렉터리 : group_vars , 파일이름 : all)
> **Logstash output config**
>
> - **logstash.conf.output.hosts** Elasticserach의 호스트명 혹은 도메인을 설정

### Logstash 설치 및 설정 대상 Remote server 항목들 확인 (디렉터리 : inventories/하위 , 파일이름 : hosts.yml)
> **서버 목록**
>
> - 신규 서버 추가시에는 **[logstash-develop-new]** 혹은 **[logstash-production-new]** 추가후 Logstash 설치 및 설정 진행
> - 모든 설정 완료 후에는 기존 **[logstash-develop]** 및 **[logstash-production]** 에 해당 서버 호스트 추가하고 *-new 호스트 그룹은 삭제


### JDK 설치 및 설정 항목들 확인 (디렉터리 : roles/jdk/vars , 파일이름 : main.yml:

> **JDK 설치 및 설정 항목**
>
> - **jdk.version** 설치하고자 하는 JDK 버전
> - **jdk.file** JDK 파일 (확장자 포함)
> - **jdk.url** JDK 파일 다운로드 URL

### Logstash 기본 설치 & 설정 항목 및 플러그인 설정 항목들 확인 (디렉터리 : roles/logstash/vars , 파일이름 : main.yml)
> **Logstash 설치 및 설정 항목**
>
> - **config.logstash.plugin.xpack** logstash.yml (환경설정 파일)에 x-pack 관련 항목을 설정할 것인지 여부
> - **config.logstash.file** 로깅 관련한 input/filter/output 파일명
> - **config.logstash.reload.automatic** config.logstash.file 을 자동으로 reload 할 것인지 여부
> - **config.logstash.reload.interval** config.logstash.file 을 자동으로 reload 할 경우 interval
> - **config.logstash.jvm.xms** JVM의 -Xms 설정값
> - **config.logstash.jvm.xmx** JVM의 -Xmx 설정값 
> - **config.plugin.xpack.security.enabled** x-pack 플러그인의 보안 보안 설정을 사용할 것인지 여부
> - **config.plugin.xpack.monitoring.enabled** x-pack 플러그인의 모니터링 기능을 사용할 것인지 여부
> - **config.input.list[].type** Kafka 메시지 type 이름
> - **config.input.list[].bootstrap_servers** Kafka Address
> - **config.input.list[].topics** Kafka 토픽이름 
> - **config.input.list[].group_id** Kafka 메시지 오프셋과 관련한 그룹 아이디 (해당 값은 동일한 Kafka 메시지를 주고받는 다른 시스템과 차별되어야 함)
> - **config.input.list[].codec** input 메시지 코덱 
> - **config.output.list[].type** Kafka 메시지 type 이름
> - **config.output.list[].index** Elasticsearch에 생성될 인덱스 이름
> - **config.output.list[].hosts** group_vars.all.logstash.conf.output.hosts
> - **config.output.list[].document_id** 클러스터링 구조일 경우 document가 중복으로 저장되지 않게끔 유니크키를 지정 
> - **config.output.list[].codec** ouput 메시지 코덱


### Smith(Morpheus) 설정 항목들 확인 (디렉터리 : roles/morpheus/vars , 파일이름 : main.yml)
> **Morpheus 설치 및 설정 항목**
>
> - **smith.url** 모피어스 알림 에이전트인 Smith 다운로드 URL


### Logstash 플러그인 설정 항목들 확인 (디렉터리 : roles/plugin/vars , 파일이름 : main.yml)
> **Logstash 플러그인 설치 및 설정 항목**
>
> - **plugin.xpack.version** X-pack 플러그인 버전
> - **plugin.xpack.file** X-pack 플러그인 파일 (확장자 포함)
> - **plugin.xpack.url** X-pack 플러그인 다운로드 URL
