<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f1754a482b6a84e07287a5b775e65b6",
  "translation_date": "2025-10-01T00:26:57+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "el"
}
-->
# Δείγμα 04: Εφαρμογές Συνομιλίας Παραγωγής με Chainlit

Ένα ολοκληρωμένο δείγμα που παρουσιάζει πολλαπλές προσεγγίσεις για τη δημιουργία εφαρμογών συνομιλίας έτοιμων για παραγωγή χρησιμοποιώντας το Microsoft Foundry Local, με σύγχρονες διεπαφές ιστού, ροές απαντήσεων και προηγμένες τεχνολογίες περιηγητή.

## Τι Περιλαμβάνεται

- **🚀 Εφαρμογή Συνομιλίας Chainlit** (`app.py`): Εφαρμογή συνομιλίας έτοιμη για παραγωγή με ροή δεδομένων
- **🌐 Επίδειξη WebGPU** (`webgpu-demo/`): Επεξεργασία AI μέσω περιηγητή με επιτάχυνση υλικού
- **🎨 Ενσωμάτωση Open WebUI** (`open-webui-guide.md`): Επαγγελματική διεπαφή τύπου ChatGPT
- **📚 Εκπαιδευτικό Σημειωματάριο** (`chainlit_app.ipynb`): Διαδραστικά εκπαιδευτικά υλικά

## Γρήγορη Εκκίνηση

### 1. Εφαρμογή Συνομιλίας Chainlit

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

Άνοιγμα στη διεύθυνση: `http://localhost:8080`

### 2. Επίδειξη WebGPU μέσω Περιηγητή

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

Άνοιγμα στη διεύθυνση: `http://localhost:5173`

### 3. Ρύθμιση Open WebUI

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

Άνοιγμα στη διεύθυνση: `http://localhost:3000`

## Μοτίβα Αρχιτεκτονικής

### Πίνακας Αποφάσεων Τοπικού vs Cloud

| Σενάριο | Σύσταση | Λόγος |
|----------|----------------|--------|
| **Ευαίσθητα Δεδομένα** | 🏠 Τοπικό (Foundry) | Τα δεδομένα δεν φεύγουν από τη συσκευή |
| **Πολύπλοκη Λογική** | ☁️ Cloud (Azure OpenAI) | Πρόσβαση σε μεγαλύτερα μοντέλα |
| **Συνομιλία σε Πραγματικό Χρόνο** | 🏠 Τοπικό (Foundry) | Χαμηλή καθυστέρηση, γρηγορότερες απαντήσεις |
| **Ανάλυση Εγγράφων** | 🔄 Υβριδικό | Τοπικό για εξαγωγή, cloud για ανάλυση |
| **Παραγωγή Κώδικα** | 🏠 Τοπικό (Foundry) | Ιδιωτικότητα + εξειδικευμένα μοντέλα |
| **Ερευνητικές Εργασίες** | ☁️ Cloud (Azure OpenAI) | Απαιτείται ευρεία βάση γνώσεων |

### Σύγκριση Τεχνολογιών

| Τεχνολογία | Χρήση | Πλεονεκτήματα | Μειονεκτήματα |
|------------|----------|------|------|
| **Chainlit** | Προγραμματιστές Python, γρήγορη πρωτοτυποποίηση | Εύκολη ρύθμιση, υποστήριξη ροής | Μόνο για Python |
| **WebGPU** | Μέγιστη ιδιωτικότητα, σενάρια εκτός σύνδεσης | Εγγενές στον περιηγητή, χωρίς ανάγκη για server | Περιορισμένο μέγεθος μοντέλου |
| **Open WebUI** | Ανάπτυξη παραγωγής, ομάδες | Επαγγελματική διεπαφή, διαχείριση χρηστών | Απαιτεί Docker |

## Προαπαιτούμενα

- **Foundry Local**: Εγκατεστημένο και σε λειτουργία ([Λήψη](https://aka.ms/foundry-local-installer))
- **Python**: Έκδοση 3.10+ με εικονικό περιβάλλον
- **Μοντέλο**: Τουλάχιστον ένα φορτωμένο (`foundry model run phi-4-mini`)
- **Περιηγητής**: Chrome/Edge με υποστήριξη WebGPU για επιδείξεις
- **Docker**: Για Open WebUI (προαιρετικό)

## Εγκατάσταση & Ρύθμιση

### 1. Ρύθμιση Περιβάλλοντος Python

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Ρύθμιση Foundry Local

```cmd
# Verify Foundry Local installation
foundry --version

# Start the service
foundry service start

# Load a model
foundry model run phi-4-mini

# Verify model is running
foundry service ps
```

## Εφαρμογές Δείγματος

### Εφαρμογή Συνομιλίας Chainlit

**Χαρακτηριστικά:**
- 🚀 **Ροή σε Πραγματικό Χρόνο**: Τα tokens εμφανίζονται καθώς δημιουργούνται
- 🛡️ **Ανθεκτικός Χειρισμός Σφαλμάτων**: Ομαλή υποβάθμιση και ανάκαμψη
- 🎨 **Σύγχρονη Διεπαφή**: Επαγγελματική διεπαφή συνομιλίας έτοιμη για χρήση
- 🔧 **Ευέλικτη Διαμόρφωση**: Μεταβλητές περιβάλλοντος και αυτόματη ανίχνευση
- 📱 **Ανταποκρινόμενος Σχεδιασμός**: Λειτουργεί σε επιτραπέζιες και κινητές συσκευές

**Γρήγορη Εκκίνηση:**
```cmd
# Run with default settings (recommended)
chainlit run samples\04\app.py -w --port 8080

# Use specific model
set MODEL=qwen2.5-7b
chainlit run samples\04\app.py -w --port 8080

# Manual endpoint configuration
set BASE_URL=http://localhost:51211
set API_KEY=your-api-key
chainlit run samples\04\app.py -w --port 8080
```

### Επίδειξη WebGPU μέσω Περιηγητή

**Χαρακτηριστικά:**
- 🌐 **AI Εγγενές στον Περιηγητή**: Χωρίς ανάγκη για server, λειτουργεί εξ ολοκλήρου στον περιηγητή
- ⚡ **Επιτάχυνση WebGPU**: Επιτάχυνση υλικού όταν είναι διαθέσιμη
- 🔒 **Μέγιστη Ιδιωτικότητα**: Τα δεδομένα δεν φεύγουν ποτέ από τη συσκευή σας
- 🎯 **Χωρίς Εγκατάσταση**: Λειτουργεί σε οποιονδήποτε συμβατό περιηγητή
- 🔄 **Ομαλή Εναλλακτική**: Εναλλαγή σε CPU αν το WebGPU δεν είναι διαθέσιμο

**Εκτέλεση:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Ενσωμάτωση Open WebUI

**Χαρακτηριστικά:**
- 🎨 **Διεπαφή τύπου ChatGPT**: Επαγγελματική, οικεία διεπαφή
- 👥 **Υποστήριξη Πολλαπλών Χρηστών**: Λογαριασμοί χρηστών και ιστορικό συνομιλιών
- 📁 **Επεξεργασία Αρχείων**: Μεταφόρτωση και ανάλυση εγγράφων
- 🔄 **Εναλλαγή Μοντέλων**: Εύκολη εναλλαγή μεταξύ διαφορετικών μοντέλων
- 🐳 **Ανάπτυξη με Docker**: Έτοιμη για παραγωγή, κοντεϊνοποιημένη ρύθμιση

**Γρήγορη Ρύθμιση:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## Αναφορά Διαμόρφωσης

### Μεταβλητές Περιβάλλοντος

| Μεταβλητή | Περιγραφή | Προεπιλογή | Παράδειγμα |
|----------|-------------|---------|----------|
| `MODEL` | Ψευδώνυμο μοντέλου προς χρήση | `phi-4-mini` | `qwen2.5-7b` |
| `BASE_URL` | Σημείο πρόσβασης Foundry Local | Αυτόματη ανίχνευση | `http://localhost:51211` |
| `API_KEY` | Κλειδί API (προαιρετικό για τοπικό) | `""` | `your-api-key` |

## Επίλυση Προβλημάτων

### Συνηθισμένα Προβλήματα

**Εφαρμογή Chainlit:**

1. **Η υπηρεσία δεν είναι διαθέσιμη:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **Σύγκρουση θυρών:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Προβλήματα περιβάλλοντος Python:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**Επίδειξη WebGPU:**

1. **Το WebGPU δεν υποστηρίζεται:**
   - Ενημερώστε σε Chrome/Edge 113+
   - Ενεργοποιήστε το WebGPU: `chrome://flags/#enable-unsafe-webgpu`
   - Ελέγξτε την κατάσταση GPU: `chrome://gpu`
   - Η επίδειξη θα εναλλαχθεί αυτόματα σε CPU

2. **Σφάλματα φόρτωσης μοντέλου:**
   - Βεβαιωθείτε ότι υπάρχει σύνδεση στο διαδίκτυο για λήψη μοντέλου
   - Ελέγξτε την κονσόλα του περιηγητή για σφάλματα CORS
   - Βεβαιωθείτε ότι εξυπηρετείτε μέσω HTTP (όχι file://)

**Open WebUI:**

1. **Η σύνδεση απορρίφθηκε:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **Τα μοντέλα δεν εμφανίζονται:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### Λίστα Ελέγχου Επικύρωσης

```cmd
# ✅ 1. Foundry Local Setup
foundry --version                    # Should show version
foundry service status               # Should show "running"
foundry model list                   # Should show loaded models
curl http://localhost:51211/v1/models  # Should return JSON

# ✅ 2. Python Environment  
python --version                     # Should be 3.10+
pip list | findstr chainlit         # Should show chainlit package
pip list | findstr openai           # Should show openai package

# ✅ 3. Application Testing
chainlit run samples\04\app.py -w --port 8080  # Should open browser
# Test WebGPU demo at localhost:5173
# Test Open WebUI at localhost:3000
```

## Προχωρημένη Χρήση

### Βελτιστοποίηση Απόδοσης

**Chainlit:**
- Χρησιμοποιήστε ροή για καλύτερη αντιληπτή απόδοση
- Εφαρμόστε pooling συνδέσεων για υψηλή ταυτόχρονη χρήση
- Κάντε cache τις απαντήσεις μοντέλου για επαναλαμβανόμενα ερωτήματα
- Παρακολουθήστε τη χρήση μνήμης με μεγάλα ιστορικά συνομιλιών

**WebGPU:**
- Χρησιμοποιήστε WebGPU για μέγιστη ιδιωτικότητα και ταχύτητα
- Εφαρμόστε ποσοτικοποίηση μοντέλου για μικρότερα μοντέλα
- Χρησιμοποιήστε Web Workers για επεξεργασία στο παρασκήνιο
- Κάντε cache τα μεταγλωττισμένα μοντέλα στην αποθήκευση του περιηγητή

**Open WebUI:**
- Χρησιμοποιήστε μόνιμους όγκους για ιστορικό συνομιλιών
- Ρυθμίστε όρια πόρων για το κοντέινερ Docker
- Εφαρμόστε στρατηγικές δημιουργίας αντιγράφων ασφαλείας για δεδομένα χρηστών
- Ρυθμίστε αντίστροφο proxy για τερματισμό SSL

### Μοτίβα Ενσωμάτωσης

**Υβριδικό Τοπικό/Cloud:**
```python
# Route based on complexity and privacy requirements
async def intelligent_routing(prompt: str, metadata: dict):
    if metadata.get("contains_pii"):
        return await foundry_local_completion(prompt)  # Privacy-sensitive
    elif len(prompt.split()) > 200:
        return await azure_openai_completion(prompt)   # Complex reasoning
    else:
        return await foundry_local_completion(prompt)  # Default local
```

**Πολυτροπικός Αγωγός:**
```python
# Combine different AI capabilities
async def analyze_document(file_path: str):
    # 1. OCR with WebGPU (browser-based)
    text = await webgpu_ocr(file_path)
    
    # 2. Analysis with Foundry Local (private)
    summary = await foundry_local_analyze(text)
    
    # 3. Enhancement with cloud (if needed)
    if summary.confidence < 0.8:
        summary = await azure_openai_enhance(summary)
    
    return summary
```

## Ανάπτυξη Παραγωγής

### Σκέψεις Ασφαλείας

- **Κλειδιά API**: Χρησιμοποιήστε μεταβλητές περιβάλλοντος, μην τα ενσωματώνετε στον κώδικα
- **Δίκτυο**: Χρησιμοποιήστε HTTPS στην παραγωγή, σκεφτείτε VPN για πρόσβαση ομάδας
- **Έλεγχος Πρόσβασης**: Εφαρμόστε αυθεντικοποίηση για Open WebUI
- **Ιδιωτικότητα Δεδομένων**: Ελέγξτε ποια δεδομένα παραμένουν τοπικά και ποια πηγαίνουν στο cloud
- **Ενημερώσεις**: Διατηρήστε το Foundry Local και τα κοντέινερ ενημερωμένα

### Παρακολούθηση και Συντήρηση

- **Έλεγχοι Υγείας**: Εφαρμόστε παρακολούθηση σημείων πρόσβασης
- **Καταγραφή**: Κεντροποιήστε τα logs από όλα τα στοιχεία
- **Μετρήσεις**: Παρακολουθήστε χρόνους απόκρισης, ποσοστά σφαλμάτων, χρήση πόρων
- **Αντίγραφα Ασφαλείας**: Τακτική δημιουργία αντιγράφων ασφαλείας δεδομένων συνομιλιών και διαμορφώσεων

## Αναφορές και Πόροι

### Τεκμηρίωση
- [Τεκμηρίωση Chainlit](https://docs.chainlit.io/) - Ολοκληρωμένος οδηγός πλαισίου
- [Τεκμηρίωση Foundry Local](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Επίσημα έγγραφα Microsoft
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - Ενσωμάτωση WebGPU
- [Τεκμηρίωση Open WebUI](https://docs.openwebui.com/) - Προχωρημένη διαμόρφωση

### Αρχεία Δείγματος
- [`app.py`](../../../../../Module08/samples/04/app.py) - Εφαρμογή Chainlit παραγωγής
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - Εκπαιδευτικό σημειωματάριο
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - Επεξεργασία AI μέσω περιηγητή
- [`open-webui-guide.md`](./open-webui-guide.md) - Πλήρης ρύθμιση Open WebUI

### Σχετικά Δείγματα
- [Τεκμηρίωση Συνεδρίας 4](../../04.CuttingEdgeModels.md) - Πλήρης οδηγός συνεδρίας
- [Δείγματα Foundry Local](https://github.com/microsoft/foundry-local/tree/main/samples) - Επίσημα δείγματα

---

**Αποποίηση ευθύνης**:  
Αυτό το έγγραφο έχει μεταφραστεί χρησιμοποιώντας την υπηρεσία αυτόματης μετάφρασης [Co-op Translator](https://github.com/Azure/co-op-translator). Παρόλο που καταβάλλουμε προσπάθειες για ακρίβεια, παρακαλούμε να έχετε υπόψη ότι οι αυτόματες μεταφράσεις ενδέχεται να περιέχουν λάθη ή ανακρίβειες. Το πρωτότυπο έγγραφο στη γλώσσα του θα πρέπει να θεωρείται η αυθεντική πηγή. Για κρίσιμες πληροφορίες, συνιστάται επαγγελματική ανθρώπινη μετάφραση. Δεν φέρουμε ευθύνη για τυχόν παρεξηγήσεις ή εσφαλμένες ερμηνείες που προκύπτουν από τη χρήση αυτής της μετάφρασης.