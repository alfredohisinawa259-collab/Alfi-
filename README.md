name: APK
on: workflow_dispatch
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Descompactar projecto
        run: unzip -o alfi-jarvis-d projeto
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.7
      - name: Compilar
        working-directory: projeto
        run: gradle assembleDebug --no-daemon
      - uses: actions/upload-artifact@v4
        with:
          name: Alfi-APK
          path: projeto/app/build/outputs/apk/debug/app-debug.apk
