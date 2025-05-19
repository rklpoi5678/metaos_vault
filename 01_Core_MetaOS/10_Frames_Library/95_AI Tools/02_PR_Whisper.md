
## 음성 독서법 독서
PDF나 EPUB을 강제 스캔하면 안되는 정책때문에
TTS나 음성지원되는것을 사용하여 
녹화후 

## 필수준비
ffmpeg 설치 후 시스템 PATH에 ffmpeg등록
Whipser설치, 필요시 torch도 필요

영상일경우 ffmpeg로 오디오추출 -> Whisper로 SST로 변환 ->DIKI 분석
음성일경우 바로 Whipser로 STT로 변환후 -> DIKI분석

## Whisper 명령어
```bash
whisper milly_tts_audio.wav --language Korean --model turbo
```
변경시 데이터 필요
그리고 1시간 미만의 녹음본 추천 (10분을 추천하지만 목적에 맞게)
#### 모델종류
tiny
base
small
medium이 속도도 적당하고 정확도도 좋음(균형)
large
turbo (속도와 효율성을 극대화한 모델 Large-v2 모델과 비슷한 수준으로 유지됨, medium보다 더 효율성이 높음)


