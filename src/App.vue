<script setup>
import { ref, computed } from 'vue'


const projectName = ref('My Premium Workspace Launcher')
const projectDescription = ref('A lightweight, responsive utility engine built to automate production workflows.')
const installationCode = ref('npm install\nnpm run dev')
const includeBadges = ref(true)


const requirements = ref([
  { id: 1, text: 'Configure local environment matrices', done: true },
  { id: 2, text: 'Optimize async server routing channels', done: false },
  { id: 3, text: 'Deploy production build assets securely', done: false }
])

const newRequirement = ref('')


const addRequirement = () => {
  if (!newRequirement.value.trim()) return
  requirements.value.push({
    id: Date.now(),
    text: newRequirement.value,
    done: false
  })
  newRequirement.value = ''
}


const copyStatus = ref('📋 Copy Compiled Markdown')
const copyMarkdown = () => {
  navigator.clipboard.writeText(compiledMarkdown.value)
  copyStatus.value = 'Copied to Clipboard! ⚡'
  setTimeout(() => {
    copyStatus.value = '📋 Copy Compiled Markdown'
  }, 2000)
}

const compiledMarkdown = computed(() => {
  let md = `# 🚀 ${projectName.value}\n\n`
  
  if (includeBadges.value) {
    md += `![Vue v3](https://img.shields.io/badge/Vue-v3.x-4fc08d?style=flat-square) ` +
          `![Vite Fast](https://img.shields.io/badge/Vite-Core-646cff?style=flat-square) ` +
          `![License MIT](https://img.shields.io/badge/License-MIT-blue?style=flat-square)\n\n`
  }
  
  md += `${projectDescription.value}\n\n`
  md += `##  Installation Instructions\n\`\`\`bash\n${installationCode.value}\n\`\`\`\n\n`
  md += `##  Project Roadmap\n`
  
  requirements.value.forEach(item => {
    md += item.done ? `* [x] ${item.text}\n` : `* [ ] ${item.text}\n`
  })
  
  return md
})
</script>

<template>
  <div class="app-wrapper">
    
    <header class="app-header">
      <h1> DevForge</h1>
      <p>A reactive Single-Page Vue studio engineered to synthesize documentation models in real-time.</p>
    </header>

    <main class="studio-desk">
      
      <section class="control-panel">
        <h3>Documentation Builder Settings</h3>
        
        <div class="control-group">
          <label>Project Heading / Title</label>
          <input type="text" v-model="projectName" placeholder="Enter workspace title...">
        </div>

        <div class="control-group">
          <label>Core Scope Summary Description</label>
          <textarea v-model="projectDescription" placeholder="What does this repository do?"></textarea>
        </div>

        <div class="control-group">
          <label>Installation Console Snippet</label>
          <textarea v-model="installationCode" class="code-entry"></textarea>
        </div>

        <div class="control-group checkbox-row">
          <input type="checkbox" id="badgeCheck" v-model="includeBadges">
          <label for="badgeCheck">Inject Standard Tech Stack Badges</label>
        </div>

        <div class="roadmap-builder">
          <label>Append Roadmap Milestones</label>
          <form @submit.prevent="addRequirement" class="input-inline-row">
            <input type="text" v-model="newRequirement" placeholder="Add custom roadmap item...">
            <button type="submit">Add</button>
          </form>
        </div>
      </section>

      <section class="output-panel">
        <div class="output-header-row">
          <h3>Interactive Content Preview</h3>
          <button @click="copyMarkdown" class="copy-btn">{{ copyStatus }}</button>
        </div>

        <pre class="markdown-preview"><code>{{ compiledMarkdown }}</code></pre>
      </section>

    </main>
  </div>
</template>

<style scoped>
.app-wrapper {
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 24px;
  font-family: system-ui, -apple-system, sans-serif;
  color: #f8fafc;
}

.app-header {
  border-bottom: 2px solid #334155;
  padding-bottom: 20px;
  margin-bottom: 35px;
}

.app-header h1 {
  margin: 0;
  font-size: 30px;
  color: #4fc08d;
  letter-spacing: -0.5px;
}

.app-header p {
  margin: 4px 0 0 0;
  color: #94a3b8;
  font-size: 14px;
}

.studio-desk {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
  gap: 40px;
}

.control-panel {
  background-color: #1e293b;
  border: 1px solid #334155;
  padding: 25px;
  border-radius: 16px;
  box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3);
}

.control-panel h3 {
  margin-top: 0;
  margin-bottom: 20px;
  font-size: 16px;
  color: #94a3b8;
  text-transform: uppercase;
}

.control-group {
  margin-bottom: 20px;
}

.control-group label {
  display: block;
  font-size: 13px;
  font-weight: 700;
  color: #cbd5e1;
  margin-bottom: 8px;
}

.control-panel input[type="text"], 
.control-panel textarea {
  width: 100%;
  padding: 10px 14px;
  background-color: #0f172a;
  border: 1px solid #334155;
  border-radius: 8px;
  color: #fff;
  font-size: 14px;
  box-sizing: border-box;
}

.control-panel textarea {
  min-height: 70px;
  resize: vertical;
}

.code-entry {
  font-family: monospace;
  color: #a7f3d0 !important;
}

.checkbox-row {
  display: flex;
  align-items: center;
  gap: 10px;
}

.checkbox-row input {
  width: 16px;
  height: 16px;
  cursor: pointer;
}

.checkbox-row label {
  margin-bottom: 0;
  cursor: pointer;
}

.input-inline-row {
  display: flex;
  gap: 10px;
  margin-top: 6px;
}

.input-inline-row button {
  padding: 0 16px;
  background-color: #4fc08d;
  color: #0f172a;
  border: none;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
}

.output-panel {
  display: flex;
  flex-direction: column;
}

.output-header-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

.output-header-row h3 {
  margin: 0;
  font-size: 16px;
  color: #94a3b8;
}

.copy-btn {
  padding: 8px 16px;
  background-color: transparent;
  border: 1px solid #4fc08d;
  color: #4fc08d;
  border-radius: 8px;
  font-weight: 700;
  font-size: 13px;
  cursor: pointer;
  transition: 0.2s;
}

.copy-btn:hover {
  background-color: #4fc08d;
  color: #0f172a;
}

.markdown-preview {
  background-color: #0f172a;
  border: 1px solid #334155;
  padding: 30px;
  border-radius: 16px;
  font-family: monospace;
  font-size: 14px;
  color: #38bdf8;
  line-height: 1.6;
  overflow-x: auto;
  margin: 0;
  flex-grow: 1;
}
</style>