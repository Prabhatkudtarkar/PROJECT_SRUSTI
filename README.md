# PROJECT_SRUSTI
port gradio as gr
from outdoor.outdoor import outdoor_detection
from indoor.indoor_module import run_indoor_finder
from reminder.reminder import setup_reminder
from dwani_api import speak_text

def run_outdoor():
    speak_text("Outdoor object detection started.")
    outdoor_detection()
    return "✅ Outdoor object detection started."

def run_indoor():
    speak_text("Indoor object finder started.")
    run_indoor_finder()
    return "✅ Indoor object finder started."

def run_reminder():
    speak_text("Medicine reminder started.")
    setup_reminder()
    return "✅ Medicine reminders activated."

with gr.Blocks(css="style.css", title="Drishti - Voice Assistant for the Visually Impaired") as app:
    gr.HTML("""
    <h1 style='text-align: center;'>👁️‍🗨️ Drishti</h1>
    <h3 style='text-align: center; color: gray;'>Voice Assistant for the Visually Impaired</h3>
    """)
    with gr.Row():
        with gr.Column(scale=1):
            gr.Markdown("## 🔧 Choose a Feature")
            btn_outdoor = gr.Button("🧭 Outdoor Detection")
            btn_indoor = gr.Button("🏠 Indoor Finder")
            btn_reminder = gr.Button("💊 Medicine Reminder")
            output_log = gr.Textbox(label="📢 System Status", lines=4, interactive=False)
        with gr.Column(scale=1):
            gr.Markdown("## 🖥️ Assistant Preview")
            gr.Image(value="preview.jpg", label="Preview", elem_id="preview-img")

    btn_outdoor.click(fn=run_outdoor, outputs=output_log)
    btn_indoor.click(fn=run_indoor, outputs=output_log)
    btn_reminder.click(fn=run_reminder, outputs=output_log)

app.launch()
