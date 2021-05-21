# Testing Unmanaged Databases
## 문제

- `managed = False`로 모델을 작성했으므로 migration 파일에도 `managed = False`로 되어있는 상태이다. 테스트를 돌리면 먼저 마이그레이션을 하게 되는데 이때는 `managed = True`인 테이블만 해당되어 unmanaged table로 선언된 테이블들이 존재하지 않는다는 오류가 발생한다.

## 해결

- 테스트를 할때만 마이그레이션 파일을 `'managed': True`로 바꿔서 테스트를 하면 테스트가 정상적으로 작동한다.

## 한계

- 하지만 foreign key와 같이 column → column_id로 model과 다르게 db에 저장되는 경우에는 칼럼을 찾지 못하므로 직접 마이그레이션 파일에서 컬럼을 추가해주어야 한다.
- 테스트를 돌려보기 위해 임시방편으로 사용할 수 있는 해결법이다.
