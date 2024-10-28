# 1. Base image 선택
FROM openjdk:17-jdk-slim

# 2. 작업 디렉토리 설정
WORKDIR /app

# 3. Gradle Wrapper와 필요한 파일 복사
COPY gradlew .
COPY gradle gradle
COPY libs libs
COPY sample sample
COPY build.gradle .
COPY settings.gradle .
COPY src src

# 4. Gradle Wrapper에 실행 권한 부여
RUN chmod +x ./gradlew

# 6. Spring Boot 애플리케이션 빌드
RUN ./gradlew bootJar

# 8. 컨테이너 시작 시 JAR 파일 실행
CMD ["java", "-jar", "/app/build/libs/Tas.jar"]