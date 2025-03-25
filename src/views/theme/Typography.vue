<script setup lang="ts">
import { ref, computed } from 'vue';

const projects = ref([
  { color: '89.3%', company: 'Cello Bello', project: 'Cello Bello - 2016', start: '19/07/2016', end: '31/12/2016', actual: '31/12/2016', owner: 'pboivin', tasks: 3, status: 'Archived' },
  { color: '98.5%', company: 'Cello Bello', project: 'Cello Bello - 2017', start: '01/01/2017', end: '31/12/2017', actual: '31/12/2017', owner: 'mjohnson', tasks: 30, status: 'Archived' },
  { color: '100.0%', company: 'Tech Nova', project: 'Tech Nova - 2018', start: '01/01/2018', end: '31/12/2018', actual: '31/12/2018', owner: 'asanders', tasks: 5, status: 'Archived' },
  { color: '100.0%', company: 'Soft Solutions', project: 'Soft Solutions - 2019', start: '01/01/2019', end: '31/12/2019', actual: '31/12/2019', owner: 'jdoe', tasks: 3, status: 'Archived' },
  { color: '21.4%', company: 'Soft Solutions', project: 'Soft Solutions - 2020', start: '01/01/2020', end: '31/12/2020', actual: '31/12/2020', owner: 'pboivin', tasks: 3, status: 'Archived' },
  { color: '9.9%', company: 'NextGen Corp', project: 'NextGen Corp - 2021', start: '01/01/2021', end: '31/12/2021', actual: '31/12/2021', owner: 'lwilson', tasks: 2, status: 'Archived' },
  { color: '9.9%', company: 'NextGen Corp', project: 'NextGen Corp - 2022', start: '01/01/2022', end: '31/12/2022', actual: '31/12/2022', owner: 'dthompson', tasks: 2, status: 'In Progress' },
  { color: '9.9%', company: 'InnovateX', project: 'InnovateX - 2023', start: '01/01/2023', end: '31/12/2023', actual: '31/12/2023', owner: 'mjohnson', tasks: 2, status: 'In Progress' },
  { color: '88.2%', company: 'InnovateX', project: 'InnovateX - 2024', start: '01/01/2024', end: '31/12/2024', actual: '31/12/2024', owner: 'asanders', tasks: 4, status: 'Proposed' },
  { color: '75.5%', company: 'Skyline Solutions', project: 'Skyline Solutions - 2025', start: '01/01/2025', end: '31/12/2025', actual: '31/12/2025', owner: 'jdoe', tasks: 6, status: 'Not Defined' },
]);
// const projects = ref([
//   { color: '89.3%', company: 'Cello Bello', project: 'Cello Bello - 2016', start: '19/07/2016', end: '31/12/2016', actual: '31/12/2016', owner: 'pboivin', tasks: 3, status: 'Archived' },
//   { color: '98.5%', company: 'Cello Bello', project: 'Cello Bello - 2017', start: '01/01/2017', end: '31/12/2017', actual: '31/12/2017', owner: 'pboivin', tasks: 30, status: 'Archived' },
//   { color: '100.0%', company: 'Cello Bello', project: 'Cello Bello - 2018', start: '01/01/2018', end: '31/12/2018', actual: '31/12/2018', owner: 'pboivin', tasks: 5, status: 'Archived' },
//   { color: '100.0%', company: 'Cello Bello', project: 'Cello Bello - 2019', start: '01/01/2019', end: '31/12/2019', actual: '31/12/2019', owner: 'pboivin', tasks: 3, status: 'Archived' },
//   { color: '21.4%', company: 'Cello Bello', project: 'Cello Bello - 2020', start: '01/01/2020', end: '31/12/2020', actual: '31/12/2020', owner: 'pboivin', tasks: 3, status: 'Archived' },
//   { color: '9.9%', company: 'Cello Bello', project: 'Cello Bello - 2021', start: '01/01/2021', end: '31/12/2021', actual: '31/12/2021', owner: 'pboivin', tasks: 2, status: 'Archived' },
//   { color: '9.9%', company: 'Cello Bello', project: 'Cello Bello - 2022', start: '01/01/2022', end: '31/12/2022', actual: '31/12/2022', owner: 'pboivin', tasks: 2, status: 'In Progress' },
//   { color: '9.9%', company: 'Cello Bello', project: 'Cello Bello - 2023', start: '01/01/2023', end: '31/12/2023', actual: '31/12/2023', owner: 'pboivin', tasks: 2, status: 'In Progress' },
// ]);

const tabs = ref(['All', 'Not Defined', 'Proposed', 'In Planning', 'In Progress', 'On Hold', 'Complete', 'Template', 'Archived', 'Gantt']);
const activeTab = ref('All');
const owners = ref(['All Users', 'pboivin', 'mjohnson', 'asanders', 'jdoe', 'lwilson', 'dthompson']);
const companies = ref(['All Companies', 'Cello Bello', 'Tech Nova', 'Soft Solutions', 'NextGen Corp', 'InnovateX', 'Skyline Solutions']);

const selectedOwner = ref('All Users');
const selectedCompany = ref('All Companies');


const filteredProjects = computed(() => {
  return projects.value.filter(project => {
    const matchesOwner = selectedOwner.value === 'All Users' || project.owner === selectedOwner.value;
    const matchesCompany = selectedCompany.value === 'All Companies' || project.company === selectedCompany.value;
    const matchesTab = activeTab.value === 'All' || project.status === activeTab.value;
    return matchesOwner && matchesCompany && matchesTab;
  });
});
</script>

<template>
  <div class="container">
    <!-- Header -->
    <div class="d-flex justify-between items-center mb-3">
      <h3 class="text-primary">Projects</h3>
    </div>

    <!-- Tabs -->
    <div class="d-flex flex-wrap gap-2 mb-3">
      <button
        v-for="tab in tabs"
        :key="tab"
        @click="activeTab = tab"
        :class="['px-4 py-2 border rounded', activeTab === tab ? 'bg-primary text-white' : 'bg-light']"
      >
        {{ tab }} ({{ filteredProjects.filter(p => p.status === tab).length }})
      </button>
    </div>

    <!-- Filters -->
    <div class="d-flex gap-3 mb-3">
      <select v-model="selectedOwner" class="border px-2 py-1">
        <option v-for="owner in owners" :key="owner" :value="owner">{{ owner }}</option>
      </select>

      <select v-model="selectedCompany" class="border px-2 py-1">
        <option v-for="company in companies" :key="company" :value="company">{{ company }}</option>
      </select>

      <button class="px-3 py-2 bg-primary text-white rounded">New Project</button>
    </div>

    <!-- Table -->
    <div class="overflow-x-auto">
      <table class="table table-striped table-bordered">
        <thead class="bg-primary text-white">
          <tr>
            <th>Color</th>
            <th>Company</th>
            <th>Project Name</th>
            <th>Start</th>
            <th>End</th>
            <th>Actual</th>
            <th>Owner</th>
            <th>Tasks (My)</th>
            <th>Selection</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="project in filteredProjects" :key="project.project">
            <td>{{ project.color }}</td>
            <td>{{ project.company }}</td>
            <td>{{ project.project }}</td>
            <td>{{ project.start }}</td>
            <td>{{ project.end }}</td>
            <td :class="{ 'text-danger': project.actual < project.end }">{{ project.actual }}</td>
            <td>{{ project.owner }}</td>
            <td>{{ project.tasks }}</td>
            <td><input type="checkbox" /></td>
            <td>{{ project.status }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Update Status -->
    <div class="d-flex gap-2 mt-3">
      <button class="px-3 py-2 bg-secondary text-white rounded">Update Project Status</button>
      <select class="border px-2 py-1">
        <option>In Planning</option>
        <option>In Progress</option>
        <option>Archived</option>
      </select>
    </div>
  </div>
</template>




<!-- <template>
  <CRow>
    <CCol>
      <CCard class="mb-4">
        <CCardHeader> Headings </CCardHeader>
        <CCardBody>
          <p>
            Documentation and examples for Bootstrap typography, including
            global settings, headings, body text, lists, and more.
          </p>
          <CTable>
            <CTableHead>
              <CTableRow>
                <CTableHeaderCell>Heading</CTableHeaderCell>
                <CTableHeaderCell>Example</CTableHeaderCell>
              </CTableRow>
            </CTableHead>
            <CTableBody>
              <CTableRow>
                <CTableDataCell>
                  <p>
                    <code class="highlighter-rouge">
                      &lt;h1&gt;&lt;/h1&gt;
                    </code>
                  </p>
                </CTableDataCell>
                <CTableDataCell
                  ><span class="h1">h1. Bootstrap heading</span></CTableDataCell
                >
              </CTableRow>
              <CTableRow>
                <CTableDataCell>
                  <p>
                    <code class="highlighter-rouge">
                      &lt;h2&gt;&lt;/h2&gt;
                    </code>
                  </p>
                </CTableDataCell>
                <CTableDataCell
                  ><span class="h2">h2. Bootstrap heading</span></CTableDataCell
                >
              </CTableRow>
              <CTableRow>
                <CTableDataCell>
                  <p>
                    <code class="highlighter-rouge">
                      &lt;h3&gt;&lt;/h3&gt;
                    </code>
                  </p>
                </CTableDataCell>
                <CTableDataCell
                  ><span class="h3">h3. Bootstrap heading</span></CTableDataCell
                >
              </CTableRow>
              <CTableRow>
                <CTableDataCell>
                  <p>
                    <code class="highlighter-rouge">
                      &lt;h4&gt;&lt;/h4&gt;
                    </code>
                  </p>
                </CTableDataCell>
                <CTableDataCell
                  ><span class="h4">h4. Bootstrap heading</span></CTableDataCell
                >
              </CTableRow>
              <CTableRow>
                <CTableDataCell>
                  <p>
                    <code class="highlighter-rouge">
                      &lt;h5&gt;&lt;/h5&gt;
                    </code>
                  </p>
                </CTableDataCell>
                <CTableDataCell
                  ><span class="h5">h5. Bootstrap heading</span></CTableDataCell
                >
              </CTableRow>
              <CTableRow>
                <CTableDataCell>
                  <p>
                    <code class="highlighter-rouge">
                      &lt;h6&gt;&lt;/h6&gt;
                    </code>
                  </p>
                </CTableDataCell>
                <CTableDataCell
                  ><span class="h6">h6. Bootstrap heading</span></CTableDataCell
                >
              </CTableRow>
            </CTableBody>
          </CTable>
        </CCardBody>
      </CCard>
      <CCard class="mb-4">
        <CCardHeader> Headings </CCardHeader>
        <CCardBody>
          <p>
            <code class="highlighter-rouge">.h1</code> through
            <code class="highlighter-rouge">.h6</code>
            classes are also available, for when you want to match the font
            styling of a heading but cannot use the associated HTML element.
          </p>
          <div class="bd-example">
            <p class="h1">h1. Bootstrap heading</p>
            <p class="h2">h2. Bootstrap heading</p>
            <p class="h3">h3. Bootstrap heading</p>
            <p class="h4">h4. Bootstrap heading</p>
            <p class="h5">h5. Bootstrap heading</p>
            <p class="h6">h6. Bootstrap heading</p>
          </div>
        </CCardBody>
      </CCard>
      <CCard class="mb-4">
        <CCardHeader> Display headings </CCardHeader>
        <CCardBody>
          <p>
            Traditional heading elements are designed to work best in the meat
            of your page content. When you need a heading to stand out, consider
            using a <strong>display heading</strong>—a larger, slightly more
            opinionated heading style.
          </p>
          <div class="bd-example bd-example-type">
            <CTable>
              <CTableBody>
                <CTableRow>
                  <CTableDataCell
                    ><span class="display-1">Display 1</span></CTableDataCell
                  >
                </CTableRow>
                <CTableRow>
                  <CTableDataCell
                    ><span class="display-2">Display 2</span></CTableDataCell
                  >
                </CTableRow>
                <CTableRow>
                  <CTableDataCell
                    ><span class="display-3">Display 3</span></CTableDataCell
                  >
                </CTableRow>
                <CTableRow>
                  <CTableDataCell
                    ><span class="display-4">Display 4</span></CTableDataCell
                  >
                </CTableRow>
              </CTableBody>
            </CTable>
          </div>
        </CCardBody>
      </CCard>
      <CCard class="mb-4">
        <CCardHeader> Inline text elements </CCardHeader>
        <CCardBody>
          <p>
            Traditional heading elements are designed to work best in the meat
            of your page content. When you need a heading to stand out, consider
            using a <strong>display heading</strong>—a larger, slightly more
            opinionated heading style.
          </p>
          <div class="bd-example">
            <p>You can use the mark tag to <mark>highlight</mark> text.</p>
            <p>
              <del>
                This line of text is meant to be treated as deleted text.
              </del>
            </p>
            <p>
              <s>
                This line of text is meant to be treated as no longer accurate.
              </s>
            </p>
            <p>
              <ins>
                This line of text is meant to be treated as an addition to the
                document.
              </ins>
            </p>
            <p><u>This line of text will render as underlined</u></p>
            <p>
              <small>
                This line of text is meant to be treated as fine print.
              </small>
            </p>
            <p>
              <strong>This line rendered as bold text.</strong>
            </p>
            <p><em>This line rendered as italicized text.</em></p>
          </div>
        </CCardBody>
      </CCard>
      <CCard class="mb-4">
        <CCardHeader> Description list alignment </CCardHeader>
        <CCardBody>
          <p>
            Align terms and descriptions horizontally by using our grid system’s
            predefined classes (or semantic mixins). For longer terms, you can
            optionally add a
            <code class="highlighter-rouge">.text-truncate</code>
            class to truncate the text with an ellipsis.
          </p>
          <div class="bd-example">
            <dl class="row">
              <dt class="col-sm-3">Description lists</dt>
              <dd class="col-sm-9">
                A description list is perfect for defining terms.
              </dd>

              <dt class="col-sm-3">Euismod</dt>
              <dd class="col-sm-9">
                <p>
                  Vestibulum id ligula porta felis euismod semper eget lacinia
                  odio sem nec elit.
                </p>
                <p>Donec id elit non mi porta gravida at eget metus.</p>
              </dd>

              <dt class="col-sm-3">Malesuada porta</dt>
              <dd class="col-sm-9">
                Etiam porta sem malesuada magna mollis euismod.
              </dd>

              <dt class="col-sm-3 text-truncate">
                Truncated term is truncated
              </dt>
              <dd class="col-sm-9">
                Fusce dapibus, tellus ac cursus commodo, tortor mauris
                condimentum nibh, ut fermentum massa justo sit amet risus.
              </dd>

              <dt class="col-sm-3">Nesting</dt>
              <dd class="col-sm-9">
                <dl class="row">
                  <dt class="col-sm-4">Nested definition list</dt>
                  <dd class="col-sm-8">
                    Aenean posuere, tortor sed cursus feugiat, nunc augue nunc.
                  </dd>
                </dl>
              </dd>
            </dl>
          </div>
        </CCardBody>
      </CCard>
    </CCol>
  </CRow>
</template> -->
