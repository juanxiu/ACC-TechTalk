FROM openjdk:17-jdk-slim

# JAR 파일을 지정된 경로로 복사
ARG JAR_FILE=build/libs/acc-techtalk-0.0.1-SNAPSHOT.jar
COPY ${JAR_FILE} /app/app.jar

# 애플리케이션 실행
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
