.. raw:: html

  <div>
    <table id="packages">
      {% for section, packages in config | dictsort %}
      <tr>
        <th colspan=5>
          {% with section_id = section | lower | replace(" ", "-") %}
          <h3 id="{{ section_id }}">
            {{ section }}
            <a class="headerlink" href="#{{ section_id }}" title="Permalink to this headline">#</a>
          </h3>
          {% endwith %}
        </th>
      </tr>

      {% for package in packages | sort(attribute="repo_name") %}
      <tr>
        <td>
          <a href="{{ package.repo }}">
            <img src="_static/badges/code-gray.svg" alt="code badge" class="sd-bg-transparent">
          </a>
        </td>

        <td>
        {% if 'pypi' in package.badges %}
          <a href="https://pypi.org/project/{{ package.pypi_name }}">
            <img src="_static/badges/pip-orange.svg" alt="pypi badge" class="sd-bg-transparent">
          </a>
        {% endif %}
        </td>
        <td>
        {% if 'conda' in package.badges %}
          <a href="https://anaconda.org/{{ package.conda_channel }}/{{ package.conda_package }}">
          <img src="_static/badges/conda-blue.svg" alt="conda badge" class="sd-bg-transparent">
          </a>
        {% endif %}
        </td>

        <td>
        {% if 'site' in package.badges %}
          <a href="{{ package.site }}">{{ package.name }}</a>
        {% else %}
          <a href="{{ package.repo }}">{{ package.name }}</a>
        {% endif %}
        </td>
        <td>
          {{ package.description }}
        </td>

      </tr>
      {% endfor %}
      {% endfor %}
    </table>
  </div>
