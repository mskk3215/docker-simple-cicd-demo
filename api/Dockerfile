FROM gradle:7 AS base
CMD ["bash"]

# build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
# ↓一緒にテストもやってくれる仕様
RUN ./gradlew build   

# production
# openjdkはjavaを開発するための環境
FROM openjdk:17 AS production
COPY --from=test-and-build /workspace/build/libs/api-0.0.1-SNAPSHOT.jar ./api.jar
CMD ["java", "-jar", "api.jar"]
