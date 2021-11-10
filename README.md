# chromeprintbug
Reproduceable Chrome Print Bug

On current version of chrome 95.0.4638.69 (Official Build) (64-bit) - and chromium based products such as Edge - a flexbox element with a gap attribue that is hidden via a print stylesheet will cause the print-preview to believe the document is many thousands of pages long and will timeout/crash the browser tab.

If the gap attribute is remove from the stylesheet, the bug no longer occurs.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <style>
        div#test {
            display: flex;
            gap: 1px;
        }
    </style>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id='test'></div>
</body>
<script>window.print();</script>
</html>
