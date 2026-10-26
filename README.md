# cholec80-annotation-manual

`cholec80` 데이터셋에 대해 사람이 직접 보정한 수술도구 bbox/tip 어노테이션이다.

[tooltip-annotator](https://github.com/doosik71/tooltip-annotator)의
`scripts/annotation_editor.py`가 생성하고, `scripts/generate_annotation.py`가 읽는다.

## 배치 위치

이 저장소는 tooltip-annotator 작업 트리 안의 다음 경로에 클론한다.

```text
tooltip-annotator/data/dataset/cholec80/annotation-manual/
```

tooltip-annotator는 `.gitignore`로 `data/` 전체를 제외하므로, 이 저장소는 바깥 저장소와
완전히 독립적으로 동작한다. 서브모듈이 아니다.

```bash
git clone https://github.com/doosik71/cholec80-annotation-manual.git \
  tooltip-annotator/data/dataset/cholec80/annotation-manual
```

## 구조

```text
train/{stem}.json
val/{stem}.json
test/{stem}.json
```

파일 이름은 대응하는 프레임 이미지(`data/dataset/cholec80/images/{split}/{stem}.png`)와
같은 베이스명을 쓴다. 여기에 파일이 있는 프레임은 `generate_annotation.py`가 마스크를
다시 분석하지 않고 이 내용을 그대로 사용한다. 따라서 `--overwrite`로 전체를 재생성해도
보정 내용은 사라지지 않는다.

## 형식

```json
{
  "image": "video01_00000475.png",
  "width": 736,
  "height": 480,
  "source": "manual",
  "edited_at": "2026-10-26T11:12:33+09:00",
  "annotations": [
    {
      "bbox": { "x": 33, "y": 207, "width": 273, "height": 47 },
      "tip":  { "x": 305, "y": 245 }
    }
  ]
}
```

`source`는 항상 `manual`이고, `edited_at`은 편집기가 저장한 시각이다. `annotations`가 빈
배열이면 "이 프레임에는 수술도구가 없다"는 사람의 판단을 뜻한다.

## 중요

이 저장소의 내용은 **어떤 스크립트로도 다시 만들어낼 수 없다.** 자동 생성 결과는
segmentation 마스크에서 언제든 재생성되지만, 여기 담긴 보정 내용은 사람의 작업 결과다.
