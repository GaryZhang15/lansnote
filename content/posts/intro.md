---
title: "Intro"
date: 2021-08-24T21:04:57+08:00
draft: false
---

*test*

> trying to see if hugo works for me

[Text](https://www.gohugo.io "Title")


```powershell {linenos=table,linenostart=1}
// Get-Service bits
Get-Service bits
```

**sample html code**
{{< highlight html "linenos=table,linenostart=1">}}
<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
        {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{< /highlight >}}

**sample powershell code**
{{< highlight powershell "linenos=table,linenostart=1">}}
Get-Service bits
Get-Service bits
Get-Service bits
{{< /highlight >}}