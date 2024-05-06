<pre>
# miniproject-ansible
terraformInfra-ansibleService-repository <br>

# 디렉토리 설명
ci-cd - CI/CD 관련 설치 yaml파일<br>

db - db 설치 설정 jinja2 템플릿 및 플레이북<br>

docker - os 별 docker 설치 플레이북<br>

haproxy - haproxy - keepalived 고가용성 및 장애대응 설정 파일<br>

java - os 별 java 설치 플레이북<br>

kube - 쿠버네티스 인스톨 및 설정 파일<br>

utils - 유용할 수 있는 기능들 ( 설정파일 백업, log복사, hosts파일 생성, 호스트에 설치된 패키지 가져오기 )<br>

# 사용된 ansible.cfg 설정
[defaults]<br>
inventory = /home/ec2-user/.ansible/aws_ec2.yml<br>
private_key_file = 개인키 위치/ 개인 키 이름<br>
host_key_checking = False<br>

[inventory]<br>
enable_plugins = amazon.aws.aws_ec2<br>
<br>
[privilege_escalation]<br>
become = true<br>
become_method = sudo<br>
become_user = root<br>
become_ask_pass = false<br>

# 사용된 ansible dynamic inventory 구성<br>
<br>
plugin: amazon.aws.aws_ec2<br>
regions:<br>
  - "ap-south-1"<br>
keyed_groups:<br>
  - key: tags<br>
    prefix: tag<br>
  - prefix: instance_type<br>
    key: instance_type<br>
  - key: placement.region<br>
    prefix: aws_region<br>
filters:<br>
  instance-state-name: running<br>
compose:<br>
  ansible_host: private_ip_address<br>

</pre>
