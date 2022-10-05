# python-template

## package manager
```
# generate/update requirements.txt
pipreqs --force

# install packages
pip install -r requirements.txt 
```

## pylint: static code analyser 
```
pip install pylint
```
```
pylint [options] modules_or_packages
```

## RabbitMQ
```
docker run -d --restart=always --hostname my-rabbit --name rabbit -p 15672:15672 -p 5672:5672 rabbitmq
docker exec -it 容器id /bin/bash
rabbitmq-plugins enable rabbitmq_management
```
default user name / password: guest

## celery
```
celery -A tasks worker --loglevel=INFO
```

## flower
```
 pip install flower
 celery -A tasks flower --broker=amqp://guest:guest@localhost:5672// --port=5555
```
