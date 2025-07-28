#### 언리얼 AI의 핵심 요소

| 요소                     | 역할                                            |
| ---------------------- | --------------------------------------------- |
| AI Controller (뇌)      | 무엇을 할지 결정하는 곳                                 |
| Pawn/Character (몸)     | 실제로 맵에서 움직이는 메시<br>Controller의 명령을 받아 실행      |
| Navigation System (지도) | AI가 "어디로 갈 수 있는지" 알려주는 시스템<br>장애물을 피해가는 경로 계산 |
| Perception System (감각) | 시각, 청각 등 감지 시스템                               |
| Blackboard (기억)        | AI의 단기 기억 저장소<br>"플레이어 위치", "경계 상태" 등 저장      |
| Behavior Tree (행동 결정)  | IF-THEN 로직을 시각적으로 표현<br>만약 플레이어가 보이면 -> 쫓아가기  |

#### 기본 AI 생성 -아무것도 안하고 서있는 AI

```
#pragma once

#include "CoreMinimal.h"
#include "AIController.h"
#include "SpartaAIController.generated.h"

UCLASS()
class SPARTAPROJECT_API ASpartaAIController : public AAIController
{
    GENERATED_BODY()

public:
    ASpartaAIController();

protected:
    virtual void OnPossess(APawn* InPawn) override;
};
```
 
*SpartaAIContoller.h*

```
#include "SpartaAIController.h"

ASpartaAIController::ASpartaAIController()
{
}

void ASpartaAIController::OnPossess(APawn* InPawn)
{
    Super::OnPossess(InPawn);

    if (InPawn)
    {
        UE_LOG(LogTemp, Warning, TEXT("[Sparta] AI Controller is controlling %s."), *InPawn->GetName());
    }
}
```

*SpartaAICharacter.cpp*

#### Navigation 추가 - 랜덤하게 돌아다니는 AI

```
#pragma once

#include "CoreMinimal.h"
#include "AIController.h"
#include "SpartaAIController.generated.h"

UCLASS()
class SPARTAPROJECT_API ASpartaAIController : public AAIController
{
    GENERATED_BODY()

public:
    ASpartaAIController();

protected:
    virtual void BeginPlay() override;
    virtual void OnPossess(APawn* InPawn) override;

private:
    void MoveToRandomLocation();
    FTimerHandle RandomMoveTimer;

    UPROPERTY(EditAnywhere, Category = "AI")
    float MoveRadius = 1000.0f;
};
```

*SpartaAIContoller.h*

```

```