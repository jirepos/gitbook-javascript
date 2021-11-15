# bit 연산

```jsx
<script>

    // 이진수 
    // 1byte 
    // 이진수   1      1    1     1     1     1      1    1  
    // 십진수   128   64   32     16    8     4      2    1
    // 자릿수   2^7  2^6   2^5   2^4   2^3   2^ 2   2^1  2^0


    //  마지막 비트가 0 이면 
    //  2^0  * 0  = 0 
    //  2^0 =  1 
    // 마지막 비트가 1 이면 
    //  2^0 * 1 = 1 
    
    // 11 의 계산 
    // (2^1 * 1) + (2^0 * 1)
    // = (2*1) + (1 * 1)
    // =  2 + 1 = 3

    

    // AND 연산.  둘 다 참이어야 참 
    // 끝 0 승의 자리가 참인지 확인 
    // 
    let auth = 0; 
    let p = 1;
    //  auth(00000000) & p(00000001)
    let result = auth &  p;
    console.log(result);   // 결과는 0 

    // OR  연산
    result = auth || p;
    console.log(result);  // 결과는 1 

    
    // 3번째 자리가 참인지 확인하기 위해 && 연산 사용 
    // 00000100  = 4
    // 같은 수(4)를 & 연산하면 둘 다 참이어야 만 1이 된다. 
    auth = 4;
    p = 4; 
    result = auth & p 
    console.log(result)  // 결과는 4

    // Shift 연산 사용 
    // 자리수를 밀기 
    auth = 1;
    // 00000001 -->  00000010
    auth = auth << 1;
    // 결과 값은 2가 되어야 함 
    console.log(auth); // 2
    // 두자리를 밀면 4가 되어야 함 
    auth = 1
    auth = auth << 2
    console.log(auth);  // 4

    // 권한 처리 
    // 실행 1, 읽기 2, 쓰기 4인 경우 
    // 실행권한이 있으면 1 
    // 실행과 읽기 권한이 있으면 3 
    // 실행과 읽기,쓰기 권한이 있으면 7
    // 사용자가 실행권한이 있는지 확인 
    let userAuth = 1; 
    console.log(userAuth && 1); // 1 
    // 읽기 궎한이 있는지 확인
    userAuth = 3;
    console.log(userAuth & 2) // 2 
    // 아니면 
    console.log( (userAuth & (1 << 1))); // 2
  </script>
  ```