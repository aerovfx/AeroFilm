python -m venv {name}

pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
python -m pip install --upgrade pip
pip install fastapi
pip install uvicorn
pip install trimesh
pip install Pillow
pip install diffusers
pip install transformers
pip install sentencepiece
pip install -r requirements.txt  
pip3 install gradio==3.39.0

Scripts\activate
Scripts\deactivate

python gradio_app.py
python gradio_app.py --enable_t23d
