all: spark zeppelin
push: push-spark push-zeppelin
.PHONY: push push-spark push-zeppelin spark zeppelin zeppelin-build

# To bump the Spark version, bump the spark_ver in Dockerfile, bump
# this tag and reset to v1. You should also double check the native
# Hadoop libs at that point (we grab the 2.6.1 libs, which are
# appropriate for 1.5.2-with-2.6). Note that you'll need to re-test
# Zeppelin (and it may not have caught up to newest Spark).
TAG = 2.0.1_v1

# To bump the Zeppelin version, bump the version in
# zeppelin/Dockerfile and bump this tag and reset to v1.
ZEPPELIN_TAG = v0.6.2_v2

spark:
	docker build -t kykl/spark .
	docker tag kykl/spark kykl/spark:$(TAG)

# This target is useful when needing to use an unreleased version of Zeppelin
zeppelin-build:
	docker build -t kykl/zeppelin-build zeppelin-build
	docker tag kykl/zeppelin-build kykl/zeppelin-build:$(ZEPPELIN_TAG)

zeppelin:
	docker build -t kykl/zeppelin zeppelin
	docker tag kykl/zeppelin kykl/zeppelin:$(ZEPPELIN_TAG)

push-spark: spark
	docker push kykl/spark
	docker push kykl/spark:$(TAG)

push-zeppelin: zeppelin
	docker push kykl/zeppelin
	docker push kykl/zeppelin:$(ZEPPELIN_TAG)

clean:
	docker rmi kykl/spark:$(TAG) || :
	docker rmi kykl/spark || :

	docker rmi kykl/zeppelin:$(ZEPPELIN_TAG) || :
	docker rmi kykl/zeppelin || :
