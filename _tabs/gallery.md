---
# the default layout is 'page'
icon: fas fa-images
order: 4
---
> 2024.12
<!-- Start of Selection -->
<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px;">
    {% for image in site.static_files %}
        {% if image.path contains 'assets/gallery/24-12' %}
            <img src="{{ image.path | relative_url }}" alt="{{ image.name }}" style="width: 100%; height: auto;" />
        {% endif %}
    {% endfor %}
</div>


<!-- End of Selection -->



