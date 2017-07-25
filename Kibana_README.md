ansible-km-iris-kibana
=======================

[![logstash](https://img.shields.io/badge/kibana-5.5.0-blue.svg)](https://www.elastic.co/guide/en/kibana/current/introduction.html)
[![ansible](https://img.shields.io/badge/ansible-2.3-orange.svg)](https://www.ansible.com/it-automation)

## Index
1. <a href="#1-directories-schema">Directories schema</a>
2. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 실행 계정</a>
3. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 파일 및 다운로드 URL 정보</a>
4. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > Kibana 설치 및 설정 대상 서버 목록</a>
5. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > JDK 설치 및 설정</a>
6. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 기타 항목 및 플러그인 설정 항목</a>
7. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 모피어스 알림(Smith)</a>
8. <a href="">Kibana 설치 및 설정시에 사전 확인해야 할 항목 > Kibana 플러그인 설정 항목들 확인 </a>
9. <a href="">전체 설치 (디렉터리 생성, JDK 설치, Kibana설치 등)</a>
10. <a href="">Kibana만 설치</a>
11. <a href="">Kibana만 시작 / 중지 / 재시작</a>


### 1. Directories schema

Directory | desc  |
| ------------- | ------------- |
| group_vars | `Kibana`를 install하기 위한 전역 설정 값들이 정의되어 있습니다. |
| inventories  | 설치할 서버 정보가 정의되어 있습니다.  |
| roles  | 디렉터리 생성, JDK 설정 등과 같은 기본 설정과 `Kibana` 설치까지의 모든 과정이 태스크로 정의되어 있습니다. |`  
        
### 2. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 실행 계정
`디렉터리 : group_vars`  
`파일이름 : all`

items | desc  | 필수 확인
| ------------- | ------------- |---|
| account.user | 실행 계정의 아이디  |Y
| account.group  | 실행 계정의 그룹  |Y

### 3. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 파일 및 다운로드 URL 정보
```이미 설치된 Elasticsearch가 클러스터 구조일 경우 기존에 설치된 Kibana의 버전과 맞춰줘야 한다.```  
`디렉터리 : group_vars`  
`파일이름 : all`

items | desc  | 필수 확인
| ------------- | ------------- |---|
| kibana.version | 설치하고자 하는 Kibana 버전  |Y
| kibana.filename | 설치하고자 하는 Kibana 파일명 (확장자 제외)  |Y
| kibana.dirname | 설치하고자 하는 Kibana의 원본 설치 디렉터리 이름  |Y
| kibana.url | 설치하고자 하는 버전의 Kibana 다운로드 URL  |Y

### 4. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > Kibana 설치 및 설정 대상 서버 목록
`디렉터리 : inventories/하위`  
`파일이름 : main.yml`  

`신규 서버 추가시에는 [kibana-develop-new] 혹은 [kibana-production-new] 추가후 Kibana 설치 및 설정 진행`  
`모든 설정 완료 후에는 기존 [kibana-develop] 및 [kibana-production] 에 해당 서버 호스트 추가하고 *-new 호스트 그룹은 삭제`

### 5. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > JDK 설치 및 설정
```JDK가 이미 설된 경우 고려하지 않아도 된다.```  
`디렉터리 : roles/jdk/vars`  
`파일이름 : main.yml`  

items | desc  | 필수 확인
| ------------- | ------------- |---|
| jdk.version | 설치하고자하는 JDK 버전  |N
| jdk.file | JDK 파일 (확장자 포함)  |N
| jdk.url | JDK 파일 다운로드 URL  |N


### 6. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 기타 항목 및 플러그인 설정 항목
`디렉터리 : roles/kibana/vars`  
`파일이름 : main.yml`

items | desc  | 필수 확인 항목
| ------------- | ------------- |---|
| config.kibana.plugin.xpack | kibana.yml (환경설정 파일)에 x-pack 관련 항목을 설정할 것인지 여부  |Y
| config.kibana.info.list[].serverhost | Kibana가 설치될 서버 호스트  |Y
| config.kibana.info.list[].xpack | 해당 서버에 xpack을 설치할 것인지 여부|Y
| config.plugin.xpack.security.enabled | x-pack 플러그인의 보안 보안 설정을 사용할 것인지 여부  |Y
| config.plugin.xpack.monitoring.enabled | x-pack 플러그인의 모니터링 기능을 사용할 것인지 여부  |Y
| config.elasticsearch.url| Elasticsearch의 master node가 여러개일 경우 애조로에서 마스터 노드를 설정하고 해당 도메인을 사용|Y
| config.elasticsearch.requesttimeout| Request 타임아웃|N

`Kibana를 Elasticsearch와 동일한 node에 설치할 경우 config.elasticsearch.url를 **localhost** 로 정의한다.`

### 7. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > 모피어스 알림(Smith)
`디렉터리 : roles/morpheus/vars`  
`파일이름 : main.yml`

items | desc  | 필수 확인 항목
| ------------- | ------------- |---|
| smith.url | 모피어스 알림 에이전트인 Smith 다운로드 URL  |N


###  8. Kibana 설치 및 설정시에 사전 확인해야 할 항목 > Kibana 플러그인 설정 항목들 확인 
`디렉터리 : roles/plugin/vars`
`파일이름 : main.yml`

items | desc  | 필수 확인 항목
| ------------- | ------------- |---|
| plugin.xpack.version | X-pack 플러그인 버전  |Y
| plugin.xpack.file | X-pack 플러그인 파일 (확장자 포함)  |Y
| plugin.xpack.url | X-pack 플러그인 다운로드 URL  |Y

### 9. 전체 설치 (디렉터리 생성, JDK 설치, Kibana설치 등)
Develop - syntax  
```sh
ansible-playbook -i inventories/대상서버군(develop) launcher.yml --extra-vars "host=서버 호스트"
```
Develop - sample
```sh
ansible-playbook -i inventories/logstash-develop launcher.yml --extra-vars "host=kibana-develop"
```
 
Production - syntax
```sh
ansible-playbook -i inventories/대상서버군(production) launcher.yml --extra-vars "host=서버 호스트"
```
Develop - sample
```sh
ansible-playbook -i inventories/logstash-production launcher.yml --extra-vars "host=kibana-production"
```

### 10. Kibana만 설치
Logstsh - syntax
```sh
ansible-playbook -i inventories/대상서버군 kibana_setup.yml --extra-vars "host=서버 호스트"
```

### 11. Kibana만 시작 / 중지 / 재시작
Kibana - 시작
```sh
ansible-playbook -i inventories/대상서버군 kibana_start.yml --extra-vars "host=서버 호스트"
```
Kibana - 중지
```sh
ansible-playbook -i inventories/대상서버군 kibana_stop.yml --extra-vars "host=서버 호스트"
```
Kibana - 재시작
```sh
ansible-playbook -i inventories/대상서버군 kibana_restart.yml --extra-vars "host=서버 호스트"
```
