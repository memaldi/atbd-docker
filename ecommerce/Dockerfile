FROM spark:python3

USER root
RUN apt update && apt install -y unzip
RUN pip install kafka-python pyspark

USER spark
ADD generate-ecommerce-events.py /opt/spark/work-dir
RUN mkdir /opt/spark/work-dir/input
ADD ecommerce_data.orc.zip /opt/spark/work-dir/input/ecommerce_data.orc.zip

USER root 
RUN chown spark:spark /opt/spark/work-dir/generate-ecommerce-events.py
RUN chown spark:spark /opt/spark/work-dir/input/ecommerce_data.orc.zip

USER spark
RUN unzip /opt/spark/work-dir/input/ecommerce_data.orc.zip -d /opt/spark/work-dir/input
RUN rm -rf /opt/spark/work-dir/input/ecommerce_data.orc.zip


WORKDIR /opt/spark/work-dir
CMD ["python3", "generate-ecommerce-events.py"]
