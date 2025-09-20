---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

{% assign images = site.static_files | where_exp: "item", "item.path contains '/assets/img/gallery/'" %}
{% assign sorted_images = images | sort: "name" %}

<div class="gallery">
  {% capture current_month %}{% endcapture %}
  {% for image in sorted_images %}
    {% assign image_date = image.name | slice: 0, 8 %}
    {% assign image_year = image_date | slice: 0, 4 %}
    {% assign image_month = image_date | slice: 4, 2 %}
    {% capture new_month %}{{ image_year }}年{{ image_month }}月{% endcapture %}

    {% if new_month != current_month %}
      <h2>{{ new_month }}</h2>
      {% capture current_month %}{{ new_month }}{% endcapture %}
    {% endif %}

    {% assign mod_index = forloop.index0 | modulo: 3 %}
    {% if mod_index == 0 %}
      <div class="gallery-row">
    {% endif %}

    <div class="gallery-item" style="display:inline-block; width:30%; margin-right:1%; height:0; padding-bottom:32%;">
      <img src="{{ image.path }}" alt="Image" style="width:200px; height:200px; object-fit:cover;">
    </div>

    {% if mod_index == 2 or forloop.last %}
      </div>
    {% endif %}
  {% endfor %}
</div>