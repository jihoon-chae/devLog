## 좋은 Pull Request가 중요한 이유

PR의 단위와 내용이 중요한 이유는 Pull Request를 통해 코드 리뷰를 받기 위해서다. 좋은 Pull Request를 통해 코드 리뷰를 받게 되면 다음과 같은 장점이 있다.

- 코드 리뷰를 통해 팀원 간의 코드 스타일을 맞출 수 있다.
- 직접 코딩할 때 발견하지 못 했던 위험도 발견할 수 있다.
- PR의 내용만 보고서도 변경 사항에 대해 충분히 이해할 수 있다.

이러한 원활한 코드리뷰를 진행하기 위해서는 원하는 부분이나 토의해야 할 대해 명시하는 PR이 선행되어야 한다.

## Pull Request의 크기는 얼마가 적합할까?

PR의 크기가 너무 크다면 다음과 같은 단점이 있다.

- 리뷰어의 에너지라는 리소스가 소모된다.
- 피드백을 통해 고칠 내용이 많아진다.
- 그 내용을 다시 리뷰해야 한다면 코드의 작업 속도도 느려진다.

반대로 PR의 크기를 작게한다면 하나의 PR에 소모되는 시간이 줄어들고, 빠른 피드백과 빠른 수정이 가능하다.

그래서 Cisco는 300줄 ~ 400줄을 권장하고, 뱅크샐러드에서는 최대 1000줄의 줄 수 변경이라는 제한을 두고 있다. 

## PR에는 어떤 내용이 들어가면 좋을까?

리뷰어가 코드의 문맥을 빠르게 파악할 수 있도록 PR의 내용에서 충분한 정보를 전달해야 한다.

그 내용으로는 다음과 같은 내용이 포함되면 좋다.

- 무슨 이유로 코드를 변경했는지
- 어떤 위험이나 장애가 발견되었는지
- 어떤 부분에 리뷰어가 집중하면 좋을지
- 관련 스크린샷
- 테스트 계획 또는 완료 사항

## Pull Request Template이란?

Pull Request Template은 Github/Gitlab과 같은 관리 툴을 사용한다면 풀 리퀘스트를 생성할 때 자동으로 내용을 채워준다. 

**Pull Request Template**

- 코드를 추가/변경하게 된 이유 (Motivation)
- 주요 구현 사항(Key Changes)
- 리뷰어에게 전달할 말 (To Reviewers)

세 가지로 PR 템플릿을 구성했다.

## Pull Request Template 만드는 방법

1. Github 버튼의 Add file - Create new file을 클릭해서

1. pull_request_template.md 라는 파일을 생성해준다. 위치는 사용자가 원하는 데 지정하는 것이 좋다. 숨겨진 디렉토리에 저장하기 위해 .github 하위에 저장하는 방법이 일반적이다.

```markdown
## Motivation

-

<br>

## Key Changes

-

<br>

## To Reviewers

-
```

그러면 PR을 생성할 때 PR 템플릿의 내용이 기본으로 채워진다.

## 참고자료

[https://2jinishappy.tistory.com/337](https://2jinishappy.tistory.com/337)
