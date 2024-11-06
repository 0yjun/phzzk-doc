# Database Schema

## Table: `user`

| Column Name     | Type      | Description              |
|-----------------|-----------|--------------------------|
| `id`            | integer   | 사용자 고유 ID           |
| `username`      | varchar   | 사용자 이름              |
| `role`          | varchar   | 사용자 역할 (예: 스트리머, 일반 사용자 등) |
| `created_at`    | timestamp | 사용자 생성 시간         |

---

## Table: `follow`

| Column Name      | Type    | Description                 |
|------------------|---------|-----------------------------|
| `id`             | integer | 팔로우 관계의 고유 ID       |
| `following_user_id` | integer | 팔로우 하는 사용자 ID     |
| `followed_user_id`  | integer | 팔로우 당하는 사용자 ID  |

**References**:  
- `user.id` → `follow.following_user_id`  
- `user.id` → `follow.followed_user_id`

---

## Table: `block`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 차단 관계의 고유 ID            |
| `blocker_user_id` | integer | 차단한 사용자 ID             |
| `blocked_user_id` | integer | 차단된 사용자 ID             |
| `type`          | enum    | 차단 유형 ('user', 'admin')    |

---

## Table: `stream`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 방송의 고유 ID                  |
| `user_id`       | integer | 방송을 시작한 사용자 ID        |
| `current_viewers` | integer | 현재 시청자 수                 |
| `cumulative_viewers` | integer | 누적 시청자 수                |

**References**:  
- `user.id` → `stream.user_id`

---

## Table: `video`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | uuid    | 비디오의 고유 ID                |
| `stream_id`     | integer | 관련 스트림 ID                  |
| `file_path`     | varchar | 비디오 파일의 저장 경로        |

**References**:  
- `stream.id` → `video.stream_id`

---

## Table: `view_history`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 시청 기록의 고유 ID             |
| `user_id`       | integer | 시청자 ID                       |
| `video_id`      | uuid    | 관련 비디오 ID                  |
| `last_viewed`   | timestamp | 마지막 시청 시간               |

**References**:  
- `user.id` → `view_history.user_id`  
- `video.id` → `view_history.video_id`

---

## Table: `chat`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 채팅 메시지의 고유 ID           |
| `stream_id`     | integer | 관련 스트림 ID                  |
| `user_id`       | integer | 채팅을 보낸 사용자 ID          |
| `message`       | text    | 채팅 메시지 내용                |
| `timestamp`     | timestamp | 메시지 전송 시간              |

**References**:  
- `user.id` → `chat.user_id`  
- `stream.id` → `chat.stream_id`

---

## Table: `manager`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 매니저 관계의 고유 ID           |
| `streamer_id`   | integer | 매니저가 관리하는 스트리머의 ID |
| `manager_id`    | integer | 매니저의 사용자 ID             |

**References**:  
- `user.id` → `manager.streamer_id`  
- `user.id` → `manager.manager_id`

---

## Table: `activity_ban`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 활동 정지의 고유 ID             |
| `user_id`       | integer | 활동 정지를 받은 사용자 ID     |
| `banned_user_id` | integer | 제한을 적용한 사용자 ID        |
| `start_date`    | timestamp | 활동 정지 시작 시간            |
| `end_date`      | timestamp | 활동 정지 종료 시간            |
| `ban_count`     | integer | 활동 정지 횟수                 |

**References**:  
- `user.id` → `activity_ban.user_id`  
- `user.id` → `activity_ban.banned_user_id`

---

## Table: `alarm`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 알람의 고유 ID                  |
| `sender_id`     | integer | 알람을 보낸 사용자 ID (송신자) |
| `user_id`       | integer | 알람을 받을 사용자 ID          |
| `stream_id`     | integer | 관련 스트림 ID                  |
| `message`       | varchar | 알람 메시지                     |
| `created_at`    | timestamp | 알람 생성 시간                 |
| `is_read`       | boolean | 알람 확인 여부 (기본값: false)  |
| `type`          | varchar | 알람 유형 (예: "방송 시작", "방송 종료" 등) |

**References**:  
- `user.id` → `alarm.user_id`  
- `user.id` → `alarm.sender_id`  
- `stream.id` → `alarm.stream_id`

---

## Table: `report`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 신고의 고유 ID                  |
| `reporter_id`   | integer | 신고한 시청자의 사용자 ID      |
| `streamer_id`   | integer | 신고된 스트리머의 사용자 ID    |
| `reason`        | varchar | 신고 사유 (예: 부적절한 행동)   |
| `created_at`    | timestamp | 신고 생성 시간                 |

**References**:  
- `user.id` → `report.reporter_id`  
- `user.id` → `report.streamer_id`

---

## Table: `report_attachment`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 첨부파일의 고유 ID              |
| `report_id`     | integer | 해당 신고의 ID (report와 연관)  |
| `file_path`     | varchar | 첨부파일의 경로 (동영상, 캡처)  |
| `file_type`     | varchar | 첨부파일의 타입 (예: "video", "image") |

**References**:  
- `report.id` → `report_attachment.report_id`

---

## Table: `threshold`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 임계값 고유 ID                  |
| `name`          | varchar | 임계값의 이름 (예: RETRY_COUNT, MAX_RETRY_LIMIT 등) |
| `value`         | varchar | 임계값의 설정 값 (예: 5, 100 등) |
| `status`        | varchar | 임계값의 상태 (사용 중, 사용 안 함 등) |
| `created_at`    | timestamp | 임계값 생성 시간               |
| `updated_at`    | timestamp | 임계값 마지막 수정 시간       |

---

## Table: `service`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 서비스 고유 ID                  |
| `name`          | varchar | 서비스 이름 (예: transcoding, packaging 등) |
| `description`   | text    | 서비스 설명                     |
| `created_at`    | timestamp | 서비스 생성 시간               |
| `updated_at`    | timestamp | 서비스 마지막 수정 시간       |

---

## Table: `threshold_service_usage`

| Column Name     | Type    | Description                     |
|-----------------|---------|---------------------------------|
| `id`            | integer | 관계 고유 ID                    |
| `threshold_id`  | integer | 임계값 ID (threshold 테이블과 연관) |
| `service_id`    | integer | 서비스 ID (service 테이블과 연관) |
| `in_use`        | boolean | 임계값이 서비스에서 사용 중인지 여부 |
| `created_at`    | timestamp | 임계값-서비스 관계 생성 시간    |
| `updated_at`    | timestamp | 임계값-서비스 관계 마지막 수정 시간 |

**References**:  
- `threshold.id` → `threshold_service_usage.threshold_id`  
- `service.id` → `threshold_service_usage.service_id`
