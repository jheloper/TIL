# PHP 팁

- PHP는 따로 자바의 Map이나 파이썬의 Dictionary와 같은 Key:Value를 표현하는 데이터 타입이 없다. 대신 배열, 그 중에서 연관 배열을 사용한다.
- Invalid argument supplied for foreach() 경고의 경우, foreach에 사용되는 요소가 array이나 object(?)로 특정되지 않았기 떄문이다. 따라서 이 경우 foreach 바깥에서 if문 조건 안에 is_array(), is_object()를 사용하여 요소를 검사하도록 하면 해당 경고가 사라진다.

