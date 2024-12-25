---
# the default layout is 'page'
icon: fas fa-images
order: 4
---
> 2024.11
<!-- Start of Selection -->
<div style="display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;">
    {% for image in site.static_files %}
        {% if image.path contains 'assets/album/24-11' %}
            <img src="{{ image.path | relative_url }}" alt="{{ image.name }}" style="max-width: 100%; height: auto; display: block;" />
        {% endif %}
    {% endfor %}
</div>


<!-- End of Selection -->

--

-

-


`Thank you for reading until the end.`
