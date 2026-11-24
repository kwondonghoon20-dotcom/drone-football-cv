# 채점 결과 원본

README와 실험 기록의 숫자는 모두 이 두 파일에서 나왔습니다. 평가셋은 평가 클립 2개(0144 = ClipKey 34, 0156 = ClipKey 44)의 정답 20장입니다.

## eval_results.csv: 파이프라인 전체 채점 (탐지 + 추적 + 분류)

행 하나가 실험 하나입니다.

| run | 내용 |
|---|---|
| v3_baseline | 처음 버전 (yolov8x 960 + ByteTrack + 랜덤포레스트 분류) |
| step1a_roi | v3 + ROI 재설정 |
| v4_tracker_v3cfg | + yolo26x 1920 탐지기 |
| v4 / v4_rule_* | + 추적기 튜닝, 인원 규칙 켜고 끄기 |
| v5_cnn / v5_cnn_rules | + ResNet18 팀 분류기 (인원 규칙 없음 / 있음) |
| v3_autoroi / v5_autoroi | 직접 지정 ROI 대신 자동 ROI |
| v6_yolo_ft | 파인튜닝 YOLO26m 3클래스 + 추적 |

| 열 | 뜻 |
|---|---|
| det_precision, det_recall, det_f1, TP, FP, FN | 탐지 점수 (클래스 무관, 박스 중심 거리로 정답과 짝짓기) |
| team_acc | 짝지어진 박스 중 팀까지 맞힌 비율 |
| referee_recall | 정답 심판 중 심판으로 맞힌 비율 |
| segment_unique_ids_34 / _44 | 득점 플레이 구간에 나온 추적 ID 수 |
| segment_unknown_ratio_34 / _44 | 팀이 Unknown으로 남은 박스 비율 |
| scorer_* | 득점 선수 추적 지표. ⚠️ 정답 경로가 v3에서 사람이 이어 붙인 구간이라 신뢰도가 낮아 결론에 쓰지 않음 |

## det_results.csv: 탐지기 비교 (탐지만, 추적 없음, conf 0.15)

1b 단계에서 모델(yolov8x / yolo26x), 입력 해상도(960 / 1280 / 1920), SAHI를 비교한 결과입니다. 클래스별 Recall과 선수 키(px) 구간별 Recall, 이미지 한 장당 처리 시간(T4)이 함께 있습니다.
