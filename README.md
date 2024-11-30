# msc-ai-translator

[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/msc-ai-summarization) [![DeepScan grade](https://deepscan.io/api/teams/16372/projects/28382/branches/914613/badge/grade.svg)](https://deepscan.io/dashboard#view=project&tid=16372&pid=28382&bid=914613)

&lt;msc-ai-translator /> is a web component based on Chrome Built-in AI > Language Detector API and Translator API. Web developers could use &lt;msc-ai-translator /> wrap article which want to adopt translate language feature.

![<msc-ai-translator />](https://blog.lalacube.com/mei/img/preview/msc-ai-translator.png)

## Basic Usage

&lt;msc-ai-translator /> is a web component. All we need to do is put the required script into your HTML document. Then follow &lt;msc-ai-translator />'s html structure and everything will be all set.

- Required Script

```html
<script
  type="module"
  src="https://unpkg.com/msc-ai-translator/mjs/wc-msc-ai-translator.js">        
</script>
```

- Structure

Put &lt;msc-ai-translator /> into HTML document. It will have different functions and looks with attribute mutation.

```html
<msc-ai-translator>
  <script type="application/json">
    {
      "l10n": {
        "subject": "Gemini",
        "introduction": "Here comes a translation.",
        "selectlanguage": "Select language",
        "translate": "Translate this article to 「{{language}}」"
      },
      "optionslanguage": "en"
    }
  </script>

  <!-- Put content element(s) which like to adopt translate feature here -->
  <div class="intro">
    萬代南夢宮娛樂於今日（3/16）宣布，由萬代南夢宮娛樂及
    ...
    ...
    ...
  </div>
</msc-ai-translator>
```

Otherwise, developers could also choose remoteconfig to fetch config for &lt;msc-ai-translator />.

```html
<msc-ai-translator
  remoteconfig="https://your-domain/api-path"
>
  ...
</msc-ai-translator>
```

## JavaScript Instantiation

&lt;msc-ai-translator /> could also use JavaScript to create DOM element. Here comes some examples.

```html
<script type="module">
import { MscAiTranslator } from 'https://unpkg.com/msc-ai-translator/mjs/wc-msc-ai-translator.js';

const contentElementTemplate = document.querySelector('.my-content-element-template');

// use DOM api
const nodeA = document.createElement('msc-ai-translator');
document.body.appendChild(nodeA);
nodeA.appendChild(contentElementTemplate.content.cloneNode(true));
nodeA.l10n = {
  subject: 'Gemini',
  introduction: 'Here comes a translation.',
  selectlanguage: 'Select language',
  translate: 'Translate this article to 「{{language}}」'
};

// new instance with Class
const nodeB = new MscAiTranslator();
document.body.appendChild(nodeB);
nodeB.appendChild(contentElementTemplate.content.cloneNode(true));
nodeB.l10n = {
  subject: 'Gemini',
  introduction: 'Here comes a translation.',
  selectlanguage: 'Select language',
  translate: 'Translate this article to 「{{language}}」'
};

// new instance with Class & default config
const config = {
  l10n: {
    subject: 'Gemini',
    introduction: 'Here comes a translation.',
    selectlanguage: 'Select language',
    translate: 'Translate this article to 「{{language}}」'
  }
};
const nodeC = new MscAiTranslator(config);
document.body.appendChild(nodeC);
nodeC.appendChild(contentElementTemplate.content.cloneNode(true));
</script>
```

## Style Customization

Developers could apply styles to decorate &lt;msc-ai-translator />'s looking.

```html
<style>
msc-ai-translator {
  /* dialog */
  --msc-ai-translator-dialog-background-color: rgba(255 255 255);
  --msc-ai-translator-dialog-backdrop-color: rgba(35 42 49/.6);
  --msc-ai-translator-dialog-head-text-color: rgba(35 42 49);
  --msc-ai-translator-dialog-line-color: rgba(199 205 210);
  --msc-ai-translator-dialog-close-icon-color: rgba(95 99 104);
  --msc-ai-translator-dialog-close-hover-background-color: rgba(245 248 250);
  --msc-ai-translator-dialog-introduction-color: rgba(35 42 49);
  --msc-ai-translator-content-text-color: rgba(35 42 49);
  --msc-ai-translator-content-highlight-text-color: rgba(68 71 70);
  --msc-ai-translator-content-highlight-background-color: rgba(233 238 246);
  --msc-ai-translator-content-group-background-color: rgba(241 244 248);
}
</style>
```

Delevelopers could add className - `align-container-size` to make &lt;msc-ai-translator />'s size same as container's size.（default is inline-size: 100% only）

```html
<msc-ai-translator class="align-container-size">
  ...
</msc-ai-translator>
```

Otherwise, apply pseudo class `::part(trigger)` to direct style the translate button.

```html
<style>
msc-ai-translator {
  &::part(trigger) {
    background: red;
  }

  &::part(trigger):hover {
    background: green;
  }
}
</style>
```

## Attributes

&lt;msc-ai-translator /> supports some attributes to let it become more convenience & useful.

- **disabled**

Hides the translate trigger button once set. It is `false` by default (not set).

```html
<msc-ai-translator disabled>
  ...
</msc-ai-translator>
```

- **l10n**

Set localization for title or action buttons.

`subject`：Set dialog subject.\
`introduction`：Set dialog result title.\
`selectlanguage`：Set language select title.\
`translate`：Set translate trigger button's content. Web developer could add keyword `{{language}}` in sentence, &lt;msc-ai-translator /> will replace it with the language you picked.

```html
<msc-ai-translator l10n='{"subject":"Gemini","introduction":"Here comes a translation.","selectlanguage":"Select language","translate":"Translate to {{language}}"}'>
  ...
</msc-ai-translator>
```

- **optionslanguage**

Set language select's option display language. Default is "`en`".

```html
<msc-ai-translator optionslanguage="zh-Hant">
  ...
</msc-ai-translator>
```

## Properties

| Property Name | Type | Description |
| ----------- | ----------- | ----------- |
| disabled | Boolean | Getter / Setter disabled. Hides the summarize trigger button once set. It is false by default. |
| l10n | Object | Getter / Setter localization for title or action buttons. Developers could set `subject`、`introduction`、`selectlanguage` and `translate` here. |
| available | String | Getter available. Web developers will get "`no`" if current browser doesn't support Build-in AI. |
| translation | String | Getter the last translation. |
| optionslanguage | String | Getter / Setter language select's option display language. |

## Mathods

| Mathod Signature | Description |
| ----------- | ----------- |
| translate({ content = '', useDialog = false, targetLanguage }) | Go translating. This is an async function. Default will take &lt;msc-ai-translator />'s children's text content to translate.<br /><br />Developers could set `useDialog` to decide display translation by dialog or not. |

## Event
| Event Signature | Description |
| ----------- | ----------- |
| msc-ai-translator-error | Fired when translate process error occured. Developers could gather `message` information through event.detail. |
| msc-ai-translator-process | Fired when prompt processing. |
| msc-ai-translator-process-end | Fired when prompt process end. |

## Reference
- [AI on Chrome > Built-in AI](https://developer.chrome.com/docs/ai/built-in)
- [Join the early preview program](https://docs.google.com/forms/d/e/1FAIpQLSfZXeiwj9KO9jMctffHPym88ln12xNWCrVkMY_u06WfSTulQg/viewform)
- [Built-in AI > Language Detection API](https://developer.chrome.com/docs/ai/language-detection)
- [Built-in AI > Translation API](https://developer.chrome.com/docs/ai/translator-api)
- [&lt;msc-ai-translator /> demo](https://blog.lalacube.com/mei/webComponent_msc-ai-translator.html)
- [YouTube tutorial](https://youtube.com/shorts/-SCYaeAQyUc)
- [WEBCOMPONENTS.ORG](https://www.webcomponents.org/element/msc-ai-translator)
