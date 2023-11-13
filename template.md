---

title: {{title}}

tags: {% if allTags %}{{allTags}}{% endif %}

citekey: {{citekey}}

---
### Reference
{{bibliography}}


{%- for attachment in attachments | filterby("path", "endswith", ".pdf") %}

 [{{attachment.title}}](file://{{attachment.path | replace(" ", "%20")}})  {%- endfor -%}.


### Abstract
{%- if abstractNote %}

{{abstractNote}}

{%- endif -%}.


### Notes
{%- if markdownNotes %}

{{markdownNotes}}

{%- endif -%}
.


### Annotations
{%- macro calloutHeader(type, color) -%}  
{%- if type == "highlight" -%}  
<mark style="background-color: {{color}}">Quote</mark>  
{%- endif -%}
{%- if type == "text" -%}  
Note 
{%- endif -%} 
{%- endmacro -%}
{% set newAnnotations = annotations | filterby("date", "dateafter", lastImportDate) %}
{% if newAnnotations.length > 0 %}
{% for a in newAnnotations %}
{{calloutHeader(a.type, a.color)}}
{{a.annotatedText}}
{% endfor %}
{% endif %}
