### hex 인코딩

Hex.encodeHexString()

: java에서 바이트배열을 16진 문자열로 변환하는 메서드

### HMAC

(keyed-hash Message AUthentication Code)

hash-based

1. 공개키를 이용해 보낼 데이터의 HMAC 값 생성(HMAC)
2. 데이터, 시그니처 전송
3. 공개키를 이용해 받은 데이터의 HMAC 값 생성 후 비교
    1. HMAC 해시값 일치면 정상, 불일치면 변조로 판단
    

### MAC(Message Authentication Code)

- 메시지 무결성(integrity)과 메시지 인증(authentication) 목적으로 사용
- 메시지가 내가 원하는 사람으로부터 왔는지 판단할 수 있게 해줌(key 사용)
- 공유 key로 message hash(MAC)을 만듦