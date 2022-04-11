# The official Canonical Ubuntu Bionic image is ideal from a security perspective,
# especially for the enterprises that we, the RabbitMQ team, have to deal with
FROM 3.8.0-management

ADD .plugins/rabbitmq_delayed_message_exchange-3.8.0.ez /opt/rabbitmq/plugins/

RUN rabbitmq-plugins enable rabbitmq_delayed_message_exchange
