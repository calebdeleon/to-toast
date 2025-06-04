# TRMNL Daily Vocabulary Plugin Guide
## The No-Code Approach Using GET + Sample

---

### Overview

This guide shows you how to create a TRMNL vocabulary plugin **without any programming**. Just a JSON file on GitHub and TRMNL's built-in randomization!

**What You'll Build:**
- A vocabulary flashcard that changes on each refresh
- No Python, no scripts, no automation needed
- Just JSON + GitHub + TRMNL

**Requirements:**
- TRMNL device with Developer add-on
- GitHub account (free)
- That's it!

---

## Step 1: Create Your Vocabulary JSON File

### 1.1 Create a Simple JSON File
Create a file called `vocabulary.json` with your words:

```json
{
  "cards": [
    {
      "word": "hola",
      "meaning": "hello",
      "example": "Hola, ¿cómo estás?"
    },
    {
      "word": "gracias",
      "meaning": "thank you",
      "example": "Gracias por tu ayuda."
    },
    {
      "word": "buenos días",
      "meaning": "good morning",
      "example": "Buenos días, profesor."
    },
    {
      "word": "por favor",
      "meaning": "please",
      "example": "¿Puedes ayudarme, por favor?"
    },
    {
      "word": "adiós",
      "meaning": "goodbye",
      "example": "Adiós, hasta mañana."
    },
    {
      "word": "perdón",
      "meaning": "excuse me / sorry",
      "example": "Perdón, ¿dónde está el baño?"
    },
    {
      "word": "agua",
      "meaning": "water",
      "example": "Necesito un vaso de agua."
    },
    {
      "word": "comida",
      "meaning": "food",
      "example": "La comida está deliciosa."
    }
  ]
}
```

### 1.2 Tips for Your JSON
- Add as many words as you want
- Keep the structure exactly as shown
- Each word needs: `word`, `meaning`, and `example`

---

## Step 2: Upload to GitHub

### 2.1 Create a GitHub Repository
1. Go to https://github.com
2. Click **"New repository"**
3. Name it something like `trmnl-vocabulary`
4. Make it **Public** (important!)
5. Click **"Create repository"**

### 2.2 Upload Your JSON File
1. Click **"Add file"** → **"Upload files"**
2. Upload your `vocabulary.json`
3. Click **"Commit changes"**

### 2.3 Get Your Raw URL
1. Click on `vocabulary.json` in your repository
2. Click the **"Raw"** button
3. Copy the URL - it should look like:
```
https://raw.githubusercontent.com/YOUR-USERNAME/trmnl-vocabulary/main/vocabulary.json
```

---

## Step 3: Create Your TRMNL Plugin

### 3.1 Access Plugin Creation
1. Log into TRMNL at https://usetrmnl.com
2. Go to **Plugins** tab
3. Search for **"Private Plugin"**
4. Click to create new

### 3.2 Configure Plugin Settings
- **Name**: Daily Vocabulary
- **Strategy**: ✅ **Polling** (not Webhook!)
- **Polling URL**: Paste your GitHub raw URL from Step 2.3
- Leave other settings as default
- Click **Save**

---

## Step 4: Create Your Display Template

### 4.1 Edit Markup
Click **"Edit Markup"** and use this template:

```liquid
{% comment %} Pick a random card from the array {% endcomment %}
{% assign random_card = cards | sample %}

<div class="view view--full">
  <div class="layout">
    <div class="columns">
      <div class="column">
        <div class="markdown">
          <!-- Header -->
          <span class="label">Today's Word</span>
          
          <!-- The word (large) -->
          <h1>{{ random_card.word }}</h1>
          
          <!-- Meaning -->
          <p>{{ random_card.meaning }}</p>
          
          <!-- Example -->
          <blockquote>
            "{{ random_card.example }}"
          </blockquote>
          
          <!-- Refresh time -->
          <span class="label label--small">
            Updated {{ "now" | date: "%H:%M" }}
          </span>
        </div>
      </div>
    </div>
  </div>
  
  <!-- Bottom bar -->
  <div class="title_bar">
    <span class="title">Vocabulary</span>
    <span class="instance">Language Learning</span>
  </div>
</div>
```

### 4.2 How the Magic Works
- `cards | sample` picks a random word from your array
- Each time TRMNL refreshes, it picks a new random word
- No coding required!

---

## Step 5: Set Your Refresh Rate

### 5.1 Add to Playlist
1. Go to **Playlists** in TRMNL
2. Add your new plugin to a playlist
3. Set refresh rate (e.g., every 2 hours)

### 5.2 Understanding Refresh Behavior
- **Every refresh** = new random word
- Set to 24 hours for one word per day
- Set to 4 hours for multiple words per day
- The selection is random, not sequential

---

## That's It! You're Done! 🎉

### What You've Built
- ✅ No Python needed
- ✅ No servers or automation
- ✅ Just JSON + GitHub + TRMNL
- ✅ New random word on each refresh

### Testing Your Plugin
1. Click **"Force Refresh"** in plugin settings
2. Check your TRMNL device
3. Each refresh shows a different random word

---

## Adding More Words

### Just Edit Your JSON
1. Go to your GitHub repository
2. Click on `vocabulary.json`
3. Click the pencil icon to edit
4. Add more words:

```json
{
  "word": "mesa",
  "meaning": "table", 
  "example": "Los libros están sobre la mesa."
}
```

5. Commit changes
6. TRMNL automatically gets the updated file

---

## Optional Enhancements

### Add More Fields
```json
{
  "cards": [
    {
      "word": "difícil",
      "meaning": "difficult",
      "example": "Este ejercicio es muy difícil.",
      "pronunciation": "dee-FEE-seel",
      "category": "adjectives",
      "difficulty": "intermediate"
    }
  ]
}
```

### Display Additional Fields
```liquid
{% assign random_card = cards | sample %}

<h1>{{ random_card.word }}</h1>
{% if random_card.pronunciation %}
  <span class="label">[{{ random_card.pronunciation }}]</span>
{% endif %}
<p>{{ random_card.meaning }}</p>
{% if random_card.category %}
  <span class="label label--small">{{ random_card.category }}</span>
{% endif %}
```

---

## Troubleshooting

### Not Seeing Words?
1. Check your GitHub URL is the "raw" version
2. Make sure repository is public
3. Try "Force Refresh" in plugin settings
4. Check JSON syntax is valid

### Same Word Appearing?
- This is random selection, not sequential
- Words can repeat by chance
- Add more words to reduce repetition
- Or adjust refresh rate

---

## Pro Tips

### 1. Organize by Difficulty
Create multiple JSON files:
- `beginner.json`
- `intermediate.json` 
- `advanced.json`

Switch URLs in TRMNL as you progress!

### 2. Theme Your Vocabulary
- `food-vocabulary.json`
- `travel-vocabulary.json`
- `business-vocabulary.json`

### 3. Track Your Learning
Add a "learned" field and update periodically:
```json
{
  "word": "coche",
  "meaning": "car",
  "example": "Mi coche es rojo.",
  "learned": true
}
```

---

## The Complete No-Code Solution

**Total Setup Time: ~10 minutes**

1. Create JSON file ✓
2. Upload to GitHub ✓  
3. Create TRMNL plugin ✓
4. Paste template ✓
5. Done! ✓

No Python, no servers, no webhooks, no automation needed. Just pure simplicity!

**Happy Learning! 🎓**