<script setup>
import { onMounted, onBeforeUnmount, ref, watch } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

const props = defineProps({
  colleges: {
    type: Array,
    required: true
  },
  selectedCollege: {
    type: Object,
    default: null
  }
})

const emit = defineEmits(['select-college'])

const mapContainer = ref(null)
const isExpanded = ref(false)

let map = null
const markersById = new Map()

function focusCollege(college) {
  if (!college || !map) return
  map.flyTo([college.lat, college.lng], 14, { duration: 0.8 })
  isExpanded.value = false
}

onMounted(() => {
  // Default center if no college is selected yet
  const initialCenter = props.colleges.length
    ? [props.colleges[0].lat, props.colleges[0].lng]
    : [14.5995, 120.9842]

  map = L.map(mapContainer.value).setView(initialCenter, 10)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map)

  props.colleges.forEach((college) => {
    const marker = L.marker([college.lat, college.lng]).addTo(map)

    marker.on('click', () => {
      emit('select-college', college)
      focusCollege(college)
    })

    markersById.set(college.id, marker)
  })

  if (props.selectedCollege) {
    focusCollege(props.selectedCollege)
  } else if (props.colleges.length > 1) {
    const bounds = L.latLngBounds(props.colleges.map((college) => [college.lat, college.lng]))
    map.fitBounds(bounds, { padding: [36, 36], maxZoom: 10 })
  }
})

watch(
  () => props.selectedCollege,
  (newCollege) => {
    if (newCollege) {
      focusCollege(newCollege)
    }
  }
)

onBeforeUnmount(() => {
  if (map) {
    map.remove()
    map = null
  }
})
</script>

<template>
  <section id="map-section" class="map-section">
    <div class="map-layout">
      <div ref="mapContainer" class="map-canvas"></div>

      <!-- Minimal Click-to-Show & Expandable Box (Blank Data Placeholder) -->
      <aside v-if="selectedCollege" class="info-panel">
        <div class="panel-header">
          <h3>{{ selectedCollege.name }}</h3>
          <button type="button" class="toggle-btn" @click="isExpanded = !isExpanded">
            {{ isExpanded ? 'Collapse' : 'Expand' }}
          </button>
        </div>

        <p class="placeholder-note">Pin selected (details intentionally left blank for now).</p>

        <div v-if="isExpanded" class="expanded-box">
          <p>Expanded view placeholder — add fields or layout later.</p>
        </div>
      </aside>

      <aside v-else class="info-panel empty-panel">
        <p>Click a pin on the map or search a school in the top bar.</p>
      </aside>
    </div>
  </section>
</template>

<style scoped>
.map-section {
  width: 100%;
  max-width: 460px;
  justify-self: center;
  padding: 0;
  background-color: transparent;
  color: #1e293b;
  font-family: Georgia, 'Times New Roman', serif;
}

.map-layout {
  max-width: 100%;
  margin: 0;
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
  align-items: start;
}

.map-canvas {
  width: 100%;
  height: auto;
  aspect-ratio: 1;
  border-radius: 12px;
  overflow: hidden;
  border: 4px solid #ffb300;
  z-index: 1;
}

.info-panel {
  background: #ffffff;
  border-radius: 12px;
  padding: 18px;
  border: 1px solid #cbd5e1;
}

.empty-panel {
  color: #475569;
  font-style: italic;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 12px;
}

.panel-header h3 {
  margin: 0;
  font-size: 1.15rem;
}

.toggle-btn {
  background: #464d6b;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  padding: 6px 12px;
  cursor: pointer;
  font-size: 0.85rem;
  flex-shrink: 0;
}

.placeholder-note {
  margin: 12px 0 0;
  font-size: 0.9rem;
  color: #64748b;
}

.expanded-box {
  margin-top: 14px;
  padding: 14px;
  border-radius: 8px;
  background: #f1f5f9;
  border: 1px dashed #94a3b8;
  font-size: 0.9rem;
  color: #334155;
}

@media (max-width: 820px) {
  .map-section {
    max-width: min(100%, 460px);
  }
}
</style>