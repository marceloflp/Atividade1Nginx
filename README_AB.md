# Fazendo Teste de Carga com Apache Bench

Após o que foi feito no arquivo README_Redirecionamento.md desse repositório for concluído, é possível fazer testes de carga utilizando o Apache Bench na nossa aplicação. Para isso, sigo o tutorial abaixo.


1- Certifique-se que tem o apache2-utils instalado em sua máquina. Caso não tenha, digite o seguinte comando no terminal para baixar:
sudo apt-get install -y apache2-utils

2- Após isso, verifique se sua aplicação está funcionando corretamente com o seguinte comando:
curl http://localhost

O resultado desse comando deve ser a estrutura html da página web.

PS- Se esses passos forem executados e retornarem ser erros, já será possível realizar testes.


1º Teste: Simular requisições por conexões simultâneas.
  
  -Rode esse comando no terminal:
  ab -n 2000 -c 20 http://localhost/

  Esse comando faz 2000 requisições com 20 conexões diferentes.

  O resultado é esse:
  
  This is ApacheBench, Version 2.3 <$Revision: 1879490 $>
  Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
  Licensed to The Apache Software Foundation, http://www.apache.org/
  
  Benchmarking localhost (be patient)
  Completed 5000 requests
  Completed 10000 requests
  Completed 15000 requests
  Completed 20000 requests
  Completed 25000 requests
  Completed 30000 requests
  Completed 35000 requests
  Finished 37864 requests
  
  
  Server Software:        nginx/1.18.0
  Server Hostname:        localhost
  Server Port:            80
  
  Document Path:          /
  Document Length:        384 bytes
  
  Concurrency Level:      10
  Time taken for tests:   10.000 seconds
  Complete requests:      37864
  Failed requests:        0
  Total transferred:      23702864 bytes
  HTML transferred:       14539776 bytes
  Requests per second:    3786.31 [#/sec] (mean)
  Time per request:       2.641 [ms] (mean)
  Time per request:       0.264 [ms] (mean, across all concurrent requests)
  Transfer rate:          2314.67 [Kbytes/sec] received
  
  Connection Times (ms)
                min  mean[+/-sd] median   max
  Connect:        0    1   0.2      1       8
  Processing:     0    2   0.4      2      11
  Waiting:        0    1   0.4      1      11
  Total:          1    3   0.5      2      13
  ERROR: The median and mean for the total time are more than twice the standard
         deviation apart. These results are NOT reliable.
  
  Percentage of the requests served within a certain time (ms)
    50%      2
    66%      3
    75%      3
    80%      3
    90%      3
    95%      3
    98%      4
    99%      5
   100%     13 (longest request)


2º Teste: Ajustando a Duração do Teste
  -Rode esse comando no terminal:
  ab -n 1000 -c 10 -t 10 http://localhost/

  Neste caso, ele fará 1000 requisições ou continuará o teste por 10 segundos, o que ocorrer primeiro.

  O resultado é esse:
  This is ApacheBench, Version 2.3 <$Revision: 1879490 $>
  Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
  Licensed to The Apache Software Foundation, http://www.apache.org/
  
  Benchmarking localhost (be patient)
  Completed 5000 requests
  Completed 10000 requests
  Completed 15000 requests
  Completed 20000 requests
  Completed 25000 requests
  Completed 30000 requests
  Completed 35000 requests
  Finished 37864 requests
  
  
  Server Software:        nginx/1.18.0
  Server Hostname:        localhost
  Server Port:            80
  
  Document Path:          /
  Document Length:        384 bytes
  
  Concurrency Level:      10
  Time taken for tests:   10.000 seconds
  Complete requests:      37864
  Failed requests:        0
  Total transferred:      23702864 bytes
  HTML transferred:       14539776 bytes
  Requests per second:    3786.31 [#/sec] (mean)
  Time per request:       2.641 [ms] (mean)
  Time per request:       0.264 [ms] (mean, across all concurrent requests)
  Transfer rate:          2314.67 [Kbytes/sec] received
  
  Connection Times (ms)
                min  mean[+/-sd] median   max
  Connect:        0    1   0.2      1       8
  Processing:     0    2   0.4      2      11
  Waiting:        0    1   0.4      1      11
  Total:          1    3   0.5      2      13
  ERROR: The median and mean for the total time are more than twice the standard
         deviation apart. These results are NOT reliable.
  
  Percentage of the requests served within a certain time (ms)
    50%      2
    66%      3
    75%      3
    80%      3
    90%      3
    95%      3
    98%      4
    99%      5
   100%     13 (longest request)
