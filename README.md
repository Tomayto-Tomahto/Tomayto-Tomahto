# tomaytomahto 🍅 | Your Personal AI Pronunciation Coach

Globalization across the entire world affects the cultures and populations, while distances between nations get shorter and shorter, language differences still define the borders. In today’s world, millions of people are trying to learn new languages every day through new and developed language learning tools. When learning a new language, the last objective we focus on is how we pronounce the words, and even if a language is well known, mispronunciation often leads to miscommunication. The goal of this project is to develop a pronunciation coach that helps people to improve their speaking skills by providing feedback and correcting their pronunciation mistakes. In order to do this, we applied various techniques based on machine learning on the dataset we created by using text-to-speech services, and we end up with a model that uses support vector machines (SVM) which can detect mispronunciations made by native Turkish speaker from native American-English speakers with an F1-Score of 93.56% as our highest on a test sample made of real voice recordings.
Keywords: Mispronunciation detection, machine learning, signal processing, text-to-speech

🎓 Developed in **2020** as the **graduation project** of the Computer Science BSc program at **Hacettepe University**.

## 🎬 Watch It in Action

[![Demo video](https://img.youtube.com/vi/tlrknc6Zf6I/0.jpg)](https://www.youtube.com/watch?v=tlrknc6Zf6I)

## 🔊 How It Works

1. **Record** — the web UI (Flask + Materialize, with an animated mic) shows you a practice word and records your pronunciation in the browser
2. **Trim** — a custom onset-detection pass finds where speech actually starts and ends, cutting the silence
3. **Extract features** — using [librosa](https://librosa.org/): chroma (STFT, CQT, CENS), RMS energy, spectral centroid / bandwidth / rolloff, zero-crossing rate, and 13 MFCCs split into per-segment chunks along the word
4. **Classify** — an SVM (RBF kernel, scikit-learn) is trained per word on features from native English vs Turkish-accented reference recordings; your recording's probability of being "native" becomes your **score**
5. **Localize mistakes** — the model is re-evaluated with individual word segments held out; if your score jumps without a segment, that's the part you likely mispronounced 🎯
6. **Visualize** — matplotlib waveform plots of your attempt and both references are rendered side by side so you can *see* the difference

## 🧰 Built With

- [scikit-learn](https://scikit-learn.org/) — SVM classification
- [librosa](https://librosa.org/) — audio processing & feature extraction
- [Flask](https://flask.palletsprojects.com/) — web app & API
- matplotlib · pandas · numpy — plotting & data wrangling
- Materialize CSS + Lottie — front-end

## 🚀 Running Locally

This is a Flask app — it needs a Python server (it won't work as a static page):

```bash
pip install flask scikit-learn librosa matplotlib pandas numpy scipy
python script.py  # or: flask --app script run
```

Expected project layout:

```
Tomayto-Tomahto/
├── script.py             # Flask app + audio pipeline + SVM
├── templates/
│   └── index.html        # the web UI (Jinja2 template)
└── static/
    ├── plots/            # generated waveform plots
    └── data/
        ├── en/<word>/    # native reference audio + feature CSVs
        └── tr/<word>/    # Turkish-accented reference audio + feature CSVs
```

> **Note:** the reference audio and per-word feature CSVs (`static/data/...`) are required for prediction and are not included in this repository.

---

![tomaytomahto demo](tomaytomahto.gif)
