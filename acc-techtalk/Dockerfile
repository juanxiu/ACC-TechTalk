FROM azul/zulu-openjdk-alpine:17-jre-latest AS runner

# JAR 파일을 지정된 경로로 복사
ARG JAR_FILE=build/libs/*.jar
COPY ${JAR_FILE} /app/app.jar

# 작업 디렉토리 설정
WORKDIR /app

EXPOSE 80

# 애플리케이션 실행
ENTRYPOINT ["java", "-jar", "app.jar"]
