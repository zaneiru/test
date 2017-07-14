# Logstash 5.5.0 install using Ansible 2.3
---


[![logstash](https://img.shields.io/badge/Logstash-5.5.0-brightgreen.svg)](https://www.elastic.co/guide/en/logstash/current/introduction.html)
[![ansible](https://img.shields.io/badge/ansible-2.3-orange.svg)](https://www.ansible.com/it-automation)



Ansible 2.3을 이용하여 Elastic stack의 일부인 Logstash 5.5.0을 다수의 서버에 설치할 수 있습니다.  
설치 전에 필히 `수정해야 할 항목`과 설치 `Script` 사용방법을 확인한 후에 사용하시기 바랍니다.

### _Getting started_
> **Note :**
>
> - `Logstash를 start 스크립트를 이용하여 시작하기 전에 Elasticsearch를 먼저 실행하시기 바랍니다.`
> - `어떻게 할까요?`    

			
### _Directories schema_

| Directory | desc  |
| ------------- | ------------- |
| group_vars | `Logstash`를 install하기 위한 전역 설정 값들이 정의되어 있습니다. |
| inventories  | 설치할 서버 정보가 정의되어 있습니다.  |
| roels  | 디렉터리 생성, JDK 설정 등과 같은 기본 설정과 `Logstash` 설치까지의 모든 과정이 태스크로 정의되어 있습니다. |
| DB | mariaDB, postgreSQL, mysql |
| utils  | google drive, mailgun |
| devOps  | **vim**, github, sublime text, sentry, pycharm|
| business tool  | wordpress, slack, kakao|



### How?

Just start typing in the left panel.

### Buttons you might want to use

- **Quick Reference**: that's a reminder of the most basic rules of Markdown
- **HTML | Preview**: *HTML* to see the markup generated from your Markdown text, *Preview* to see how it looks like

### Most useful shortcuts

- `CTRL + O` to open files
- `CTRL + T` to open a new tab
- `CTRL + S` to save the current file or tab

### Privacy

- No data is sent to any server – everything you type stays inside your application
- The editor automatically saves what you write locally for future use.  
  If using a public computer, close all tabs before leaving the editor
