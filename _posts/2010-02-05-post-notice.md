---
title: "가이드 - 주의 창 예시"
categories:
  - Blog
tags:
  - Post Formats
  - notice
---

알림은 주변 콘텐츠를 설명하는 정보를 표시합니다. 종종 특정 세부 사항에주의를 환기시키는 데 사용됩니다.

Kramdown을 사용할 때`{: .notice}`문장 뒤에`.pot </ p>`요소에`.notice '를 할당 할 수 있습니다.

**Notice:** 방금 고객 서비스 개선을 위해 [개인 정보 보호 정책](#) 을 업데이트했습니다. 변경 사항을 검토하는 것이 좋습니다.
{: .notice}

**Primary Notice:** 기본 알림창 뒤에 ``{: .notice--primary}`` 를 붙여서 [알림 박스](#)를 만들 수 있습니다.
{: .notice--primary}

**Info Notice:** 정보 알림 박스입니다. 파란색이며 ``{: .notice--info}`` 를 입력하여 사용할 수 있습니다.
{: .notice--info}

**Warning Notice:** [주의 알림 박스](#) 입니다.
{: .notice--warning}

**Danger Notice:** [위험 알림 박스](#) 입니다.
{: .notice--danger}

**Success Notice:** [성공 알림 박스](#) 입니다. 초록색의 배경을 가지고 있습니다.
{: .notice--success}

주의 사항에 여러 단락이나 다른 요소를 포함하고 싶습니까? Liquid를 사용하여 내용을 캡처 한 다음`markdownify '로 필터링하면 좋은 방법입니다.

```html
{% raw %}{% capture notice-2 %}
#### New Site Features

* You can now have cover images on blog pages
* Drafts will now auto-save while writing
{% endcapture %}{% endraw %}

<div class="notice">{% raw %}{{ notice-2 | markdownify }}{% endraw %}</div>
```

{% capture notice-2 %}
#### New Site Features

* You can now have cover images on blog pages
* Drafts will now auto-save while writing
{% endcapture %}

<div class="notice">
  {{ notice-2 | markdownify }}
</div>

또는 캡처를 건너 뛰고 HTML 문법으로 작성할 수도 있습니다.

```html
<div class="notice">
  <h4>Message</h4>
  <p>A basic message.</p>
</div>
```

<div class="notice">
  <h4>Message</h4>
  <p>A basic message.</p>
</div>