# HTTPS and Certificates

## HTTPS의 대략적인 작동원리와 Certificate의 역할

1. HTTPS를 사용하고 싶은 웹 서버가 자신의 도메인 정보와 그와 연동된 Public Key를 CA(Certificate Authority)에게 보냄. 이것을 CSR(Certificate Signing Request)라고 하는 듯

2. CA는 이것을 검증후에 웹 서버의 도메인 정보 + Public Key를 CA 자신의 Private Key로 서명한다. 이것을 Certificate이라고 함

3. 웹 서버는 이제 이 Certificate를 설치해서 HTTPS를 사용할 수 있게 됨

4. 사용자가 웹 서버에 접속할 때 Certificate을 보고 이것을 CA의 Public Key로 검증한다. 대부분의 OS에는 Root CA의 공개키가 설치되어 있어서 브라우져가 이것을 사용하는 듯.

5. 브라우져는 이제 Certificate에 들어있는 웹 서버의 공개키로 대칭키를 암호화해서 보냄

6. 웹 서버는 이것을 자신의 비공개키로 복호화해서 대칭키를 얻음

7. 이제 사용자와 웹 서버는 이 대칭키로 데이터를 암호화해서 안전하게 통신할 수 있게 됨
