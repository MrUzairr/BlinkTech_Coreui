<script setup>
import { ref, computed } from 'vue';

const companies = ref([
  { owner: 'John Doe', name: 'Blink Tech', activeProjects: 5, archivedProjects: 11, type: 'Internal' },
  { owner: 'Jane Smith', name: 'HANDS of Central Florida', activeProjects: 4, archivedProjects: 23, type: 'Client' },
  { owner: 'Michael Johnson', name: 'Dynamic Fitness', activeProjects: 3, archivedProjects: 10, type: 'Not Applicable' },
  { owner: 'Emily Davis', name: 'St Armands Baking Company', activeProjects: 2, archivedProjects: 8, type: 'Not Applicable' },
  { owner: 'John Doe', name: 'Dr. Jeff Chirillo', activeProjects: 2, archivedProjects: 7, type: 'Client' },
  { owner: 'Sarah Wilson', name: 'Cello Bello', activeProjects: 2, archivedProjects: 6, type: 'Client' },
  { owner: 'David Martinez', name: 'Sarasota Ballet', activeProjects: 0, archivedProjects: 2, type: 'Client' },
  { owner: 'Olivia Taylor', name: 'Zone Defense', activeProjects: 0, archivedProjects: 1, type: 'Not Applicable' },
  { owner: 'Sarah Wilson', name: 'Tech Solutions', activeProjects: 6, archivedProjects: 12, type: 'Vendor' },
  { owner: 'John Doe', name: 'Green Energy Corp', activeProjects: 7, archivedProjects: 15, type: 'Supplier' },
  { owner: 'Matthew Harris', name: 'Consulting Experts', activeProjects: 3, archivedProjects: 9, type: 'Consultant' },
  { owner: 'Michael Johnson', name: 'Government Services', activeProjects: 5, archivedProjects: 20, type: 'Government' },
  { owner: 'Liam Scott', name: 'Global Innovations', activeProjects: 8, archivedProjects: 14, type: 'Client' },
  { owner: 'Sarah Wilson', name: 'NextGen AI', activeProjects: 9, archivedProjects: 22, type: 'Internal' },
  { owner: 'Charlotte Hall', name: 'Future Corp', activeProjects: 4, archivedProjects: 12, type: 'Vendor' },
  { owner: 'Mia Adams', name: 'Cloud Nexus', activeProjects: 3, archivedProjects: 5, type: 'Supplier' },
  { owner: 'Michael Johnson', name: 'Data Solutions', activeProjects: 2, archivedProjects: 4, type: 'Consultant' },
]);

const tabs = ref(['All Companies', 'Client', 'Vendor', 'Supplier', 'Consultant', 'Government', 'Internal', 'Not Applicable']);
const activeTab = ref('All Companies');

const searchQuery = ref('');
const ownerFilter = ref('All');

// Get unique owner names for filtering
const owners = computed(() => {
  return ['All', ...new Set(companies.value.map(company => company.owner))];
});

// Compute the filtered companies
const filteredCompanies = computed(() => {
  return companies.value.filter(company => {
    const matchesSearch = company.owner.toLowerCase().includes(searchQuery.value.toLowerCase());
    const matchesOwner = ownerFilter.value === 'All' || company.owner === ownerFilter.value;
    const matchesTab = activeTab.value === 'All Companies' || company.type === activeTab.value;
    return matchesSearch && matchesOwner && matchesTab;
  });
});
</script>

<template>
  <CRow>
    <CCol>
      <CCard>
        <CCardHeader>
          <CIcon icon="cil-drop" /> Company List
        </CCardHeader>
        <CCardBody>
          <div class="mb-3">
            <!-- Tabs -->
            <CRow class="mb-3">
              <CCol>
                <div class="d-flex flex-wrap gap-2">
                  <button
                    v-for="tab in tabs"
                    :key="tab"
                    @click="activeTab = tab"
                    :class="['px-4 py-2 border rounded', activeTab === tab ? 'bg-primary text-white' : 'bg-light']"
                  >
                    {{ tab }}
                  </button>
                </div>
              </CCol>
            </CRow>

            <!-- Search & Owner Filter -->
            <CRow>
              <CCol md="6" class="mb-3">
                <label class="font-semibold">Search by Owner:</label>
                <input v-model="searchQuery" type="text" class="border px-2 py-1 w-full" placeholder="Search owner..." />
              </CCol>
              <CCol md="6" class="mb-3">
                <label class="font-semibold">Filter by Owner:</label>
                <select v-model="ownerFilter" class="border px-2 py-1 w-full">
                  <option v-for="owner in owners" :key="owner" :value="owner">{{ owner }}</option>
                </select>
              </CCol>
            </CRow>
          </div>

          <!-- Table -->
          <div class="overflow-x-auto">
            <table class="table table-striped table-bordered">
              <thead class="bg-primary text-white">
                <tr>
                  <th>Owner Name</th>
                  <th>Company Name</th>
                  <th>Active Projects</th>
                  <th>Archived Projects</th>
                  <th>Type</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="company in filteredCompanies" :key="company.name">
                  <td>{{ company.owner }}</td>
                  <td>{{ company.name }}</td>
                  <td>{{ company.activeProjects }}</td>
                  <td>{{ company.archivedProjects }}</td>
                  <td>{{ company.type }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </CCardBody>
      </CCard>
    </CCol>
  </CRow>
</template>




<!-- <script setup>
import ColorTheme from './ColorTheme.vue'
</script>

<template>
  <CRow>
    <CCol>
      <CCard>
        <CCardHeader> <CIcon icon="cil-drop" /> Theme colors </CCardHeader>
        <CCardBody>
          <CRow>
            <ColorTheme color="bg-primary">
              <h6>Brand Primary Color</h6>
            </ColorTheme>
            <ColorTheme color="bg-secondary"><h6>Brand Secondary Color</h6></ColorTheme>
            <ColorTheme color="bg-success"><h6>Brand Success Color</h6></ColorTheme>
            <ColorTheme color="bg-danger"><h6>Brand Danger Color</h6></ColorTheme>
            <ColorTheme color="bg-warning"><h6>Brand Warning Color</h6></ColorTheme>
            <ColorTheme color="bg-info"><h6>Brand Info Color</h6></ColorTheme>
            <ColorTheme color="bg-light"><h6>Brand Light Color</h6></ColorTheme>
            <ColorTheme color="bg-dark"><h6>Brand Dark Color</h6></ColorTheme>
          </CRow>
        </CCardBody>
      </CCard>
    </CCol>
  </CRow>
</template> -->
