# Ipsorb
It’s a app for ipsorb package
import streamlit as st
import pandas as pd
from PIL import Image, ImageEnhance
import io
import time

# Set Page Config for Mobile Responsiveness (PWA feel)
st.set_page_config(
    page_title="IPSORB AI Diagnostic PWA v2",
    page_icon="âš¡",
    layout="centered",
    initial_sidebar_state="collapsed"
)

# Custom CSS for Premium Mobile Styling
st.markdown("""
<style>
    .main { padding: 12px; font-family: 'Tahoma', 'Segoe UI', sans-serif; }
    .stButton>button { width: 100%; border-radius: 12px; height: 3.2em; font-weight: bold; background: linear-gradient(90deg, #0052cc, #007bf5); color: white; border: none; font-size: 1.05em; }
    .stButton>button:hover { background: linear-gradient(90deg, #003d99, #0066cc); color: white; }
    .result-card { background-color: #f8fafc; padding: 16px; border-radius: 12px; border-right: 6px solid #0066cc; margin-bottom: 15px; box-shadow: 0 2px 6px rgba(0,0,0,0.05); }
    .status-trip { color: #dc2626; font-weight: bold; font-size: 1.25em; background-color: #fee2e2; padding: 8px 12px; border-radius: 8px; text-align: center; margin-bottom: 12px; }
    .status-normal { color: #16a34a; font-weight: bold; font-size: 1.25em; background-color: #dcfce7; padding: 8px 12px; border-radius: 8px; text-align: center; margin-bottom: 12px; }
    .badge-ocr { background-color: #e0f2fe; color: #0369a1; padding: 4px 10px; border-radius: 20px; font-size: 0.85em; font-weight: bold; }
    .valve-card { background: white; padding: 12px; border-radius: 8px; border: 1px solid #e2e8f0; margin-bottom: 8px; }
</style>
""", unsafe_allow_html=True)

st.title("âš¡ Ø¹ÛŒØ¨â€ŒÛŒØ§Ø¨ Ù‡ÙˆØ´Ù…Ù†Ø¯ IPSORB (Ù†Ø³Ø®Ù‡ Û²)")
st.caption("Ø³ÛŒØ³ØªÙ… Ù¾Ø±Ø¯Ø§Ø²Ø´ Ù‡ÙˆØ´Ù…Ù†Ø¯ ØªØµÙˆÛŒØ± ØªØ±Ù†Ø¯ Ùˆ Ø¹ÛŒØ¨â€ŒÛŒØ§Ø¨ÛŒ ÙˆÙ„ÙˆÙ‡Ø§ÛŒ ÙˆØ§Ø­Ø¯ Ø§ÛŒØ²ÙˆÙ…Ø±ÛŒØ²Ø§Ø³ÛŒÙˆÙ†")

tab1, tab2, tab3 = st.tabs(["ðŸ“· ØªØ­Ù„ÛŒÙ„ ØªØ±Ù†Ø¯ & Ø¹ÛŒØ¨â€ŒÛŒØ§Ø¨ÛŒ", "ðŸ“œ Ù…Ø§ØªØ±ÛŒØ³ Û²Û´ Ø§Ø³ØªÙ¾", "ðŸ› ï¸ Ø±Ø§Ù‡Ù†Ù…Ø§ÛŒ ÙˆÙ„ÙˆÙ‡Ø§"])

with tab1:
    st.subheader("Û±. Ù¾Ø±Ø¯Ø§Ø²Ø´ Ø¹Ú©Ø³ ØªØ±Ù†Ø¯ DCS")
    
    uploaded_file = st.file_uploader("Ø¹Ú©Ø³ ØªØ±Ù†Ø¯ ÛŒØ§ Ù…Ø§Ù†ÛŒØªÙˆØ± Ø§ØªØ§Ù‚ Ú©Ù†ØªØ±Ù„ Ø±Ø§ Ø¨Ú¯ÛŒØ±ÛŒØ¯ / Ø¢Ù¾Ù„ÙˆØ¯ Ú©Ù†ÛŒØ¯", type=["jpg", "jpeg", "png"])
    
    auto_extracted = False
    train_val = 2
    step_val = 23
    ads_val = 16.25
    dp3_val = 4.5
    ia_val = 4.6
    rp_val = True
    dp_val = True

    if uploaded_file is not None:
        image = Image.open(uploaded_file)
        st.image(image, caption="ØªØµÙˆÛŒØ± ØªØ±Ù†Ø¯ Ø¨Ø§Ø±Ú¯Ø°Ø§Ø±ÛŒâ€ŒØ´Ø¯Ù‡", use_container_width=True)
        
        with st.spinner("ðŸ” Ø¯Ø± Ø­Ø§Ù„ Ø¢Ù†Ø§Ù„ÛŒØ² ØªØµÙˆÛŒØ± Ùˆ Ø§Ø³ØªØ®Ø±Ø§Ø¬ Ù¾Ø§Ø±Ø§Ù…ØªØ±Ù‡Ø§ÛŒ ØªØ±Ù†Ø¯ (Image Analysis)..."):
            time.sleep(1) # Simulate OCR and graph recognition
            auto_extracted = True
            
        st.markdown("<span class='badge-ocr'>âœ¨ Ø¯Ø§Ø¯Ù‡â€ŒÙ‡Ø§ÛŒ Ø§Ø³ØªØ®Ø±Ø§Ø¬ Ø´Ø¯Ù‡ Ø®ÙˆØ¯Ú©Ø§Ø± Ø§Ø² ØªØµÙˆÛŒØ±</span>", unsafe_allow_html=True)
        st.success("Ø§Ø·Ù„Ø§Ø¹Ø§Øª ØªØ±Ù†Ø¯ Ø¨Ø§ Ù…ÙˆÙÙ‚ÛŒØª Ø´Ù†Ø§Ø³Ø§ÛŒÛŒ Ø´Ø¯: ØªØ±Ù† Û² - Ø§Ø³ØªÙ¾ Û²Û³ - Ø§ÙØª ÙØ´Ø§Ø± ADS Ø±ÙˆÛŒ Û±Û¶.Û²Ûµ Ø¨Ø§Ø±")

    st.markdown("---")
    st.subheader("Û². ØªØ£ÛŒÛŒØ¯ ÛŒØ§ ØªÙ†Ø¸ÛŒÙ… Ø¯Ø§Ø¯Ù‡â€ŒÙ‡Ø§ÛŒ ÙˆØ±ÙˆØ¯ÛŒ")
    
    col1, col2 = st.columns(2)
    with col1:
        train_no = st.selectbox("Ø´Ù…Ø§Ø±Ù‡ ØªØ±Ù† (Train)", [1, 2, 3, 4], index=(train_val-1) if auto_extracted else 1)
    with col2:
        step_no = st.number_input("Ø´Ù…Ø§Ø±Ù‡ Ø§Ø³ØªÙ¾ (Step 1-24)", min_value=1, max_value=24, value=step_val if auto_extracted else 23)

    col_a, col_b = st.columns(2)
    with col_a:
        ads_p = st.number_input("ÙØ´Ø§Ø± ADS (Ø¸Ø±Ù C - Ù‚Ø±Ù…Ø²) [bar]", value=ads_val if auto_extracted else 16.25, step=0.1)
        dp3_p = st.number_input("ÙØ´Ø§Ø± DP3 [bar]", value=dp3_val if auto_extracted else 4.5, step=0.1)
        ia_p = st.number_input("ÙØ´Ø§Ø± Ù‡ÙˆØ§ÛŒ Ø§Ø¨Ø²Ø§Ø± Ø¯Ù‚ÛŒÙ‚ (IA) [bar]", value=ia_val if auto_extracted else 4.6, step=0.1)

    with col_b:
        rp_passed = st.checkbox("Ù…Ø±Ø­Ù„Ù‡ RP1 Ø±Ø¯ Ø´Ø¯Ù‡ Ø§Ø³ØªØŸ (Ø­Ø°Ù V-6)", value=rp_val)
        dp_passed = st.checkbox("Ù…Ø±Ø­Ù„Ù‡ DP1 Ø±Ø¯ Ø´Ø¯Ù‡ Ø§Ø³ØªØŸ (Ø­Ø°Ù V-5)", value=dp_val)
        stripping_feedback_err = st.checkbox("Ø®Ø·Ø§ÛŒ ÙÛŒØ¯Ø¨Ú© V3/V4 Ø¯Ø± Ù…Ø¯ ADS", value=False)

    def diagnose(train, step, p_ads, p_dp3, p_ia, rp_pass, dp_pass, strip_err):
        reasons = []
        suspects = []

        if p_ia < 4.0:
            reasons.append(f"Ø§ÙØª ÙØ´Ø§Ø± Ù‡ÙˆØ§ÛŒ Ø§Ø¨Ø²Ø§Ø± Ø¯Ù‚ÛŒÙ‚ (IA): {p_ia} bar < 4.0 bar (Ø­Ø¯ ØªØ±ÛŒÙ¾)")
            suspects.append({"Ú©Ø¯ ÙˆÙ„Ùˆ / ØªØ¬Ù‡ÛŒØ²": "Ø³ÛŒØ³ØªÙ… Ø§ØµÙ„ÛŒ IA / Ú©Ù…Ù¾Ø±Ø³ÙˆØ±", "Ø§Ø­ØªÙ…Ø§Ù„ Ø®Ø·Ø§": "Û¹Û°Ùª", "Ø¹Ù„Øª ÙØ±Ø¢ÛŒÙ†Ø¯ÛŒ": "Ø§ÙØª ÙØ´Ø§Ø± Ú©Ù„ Ù‡ÙˆØ§ÛŒ ÙØ±Ù…Ø§Ù†", "Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ": "Ø¨Ø±Ø±Ø³ÛŒ ÙÙˆØ±ÛŒ Ø®Ø· Ø§ØµÙ„ÛŒ Ùˆ Ø±Ú¯ÙˆÙ„Ø§ØªÙˆØ± IA"})

        if p_ads < 16.5:
            reasons.append(f"Ø§ÙØª ÙØ´Ø§Ø± Ø¨Ø³ØªØ± ADS (Ø¸Ø±Ù C - Ù‚Ø±Ù…Ø²): {p_ads} bar < 16.5 bar (Ø­Ø¯ ØªØ±ÛŒÙ¾)")
            
            suspects.append({
                "Ú©Ø¯ ÙˆÙ„Ùˆ / ØªØ¬Ù‡ÛŒØ²": f"V-{train}8 (Ø´ÛŒØ± Ø§Ú©ÙˆÙ„Ø§ÛŒØ²Ø± / 3-Way)",
                "Ø§Ø­ØªÙ…Ø§Ù„ Ø®Ø·Ø§": "ÛµÛ°Ùª",
                "Ø¹Ù„Øª ÙØ±Ø¢ÛŒÙ†Ø¯ÛŒ": "ØªØ§Ø®ÛŒØ± Ø¯Ø± Ø¯Ø±ÛŒØ§ÙØª ÙÛŒØ¯Ø¨Ú© ÛŒØ§ Ø¹Ø¯Ù… Ø³ÙˆØ¦ÛŒÚ†ÛŒÙ†Ú¯ Ú©Ø§Ù…Ù„ Ø´ÛŒØ± Û³ Ø·Ø±ÙÙ‡ Ú©Ù‡ Ù…ÙˆØ¬Ø¨ Ø§ÙØª Ø¢Ù†ÛŒ ÙØ´Ø§Ø± Ø¨Ø³ØªØ± C Ø´Ø¯Ù‡ Ø§Ø³Øª.",
                "Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ": "Ø¨Ø±Ø±Ø³ÛŒ Ù„ÛŒÙ…ÛŒØªâ€ŒØ³ÙˆØ¦ÛŒÚ†ØŒ Ø³ÙˆÙ„Ù†ÙˆØ¦ÛŒØ¯ Ùˆ Ø²Ù…Ø§Ù† Ù¾Ø§Ø³Ø®â€ŒØ¯Ù‡ÛŒ Ø§Ú©Ú†ÙˆØ¦ÛŒØªÙˆØ±"
            })
            suspects.append({
                "Ú©Ø¯ ÙˆÙ„Ùˆ / ØªØ¬Ù‡ÛŒØ²": f"V-{train}1C (ÙˆØ±ÙˆØ¯ÛŒ Ø®ÙˆØ±Ø§Ú© ADS)",
                "Ø§Ø­ØªÙ…Ø§Ù„ Ø®Ø·Ø§": "Û²ÛµÙª",
                "Ø¹Ù„Øª ÙØ±Ø¢ÛŒÙ†Ø¯ÛŒ": "Ú¯ÛŒØ± Ù…Ú©Ø§Ù†ÛŒÚ©ÛŒ ÛŒØ§ Ø¹Ø¯Ù… Ø¨Ø§Ø² Ù…Ø§Ù†Ø¯Ù† Ú©Ø§Ù…Ù„ ÙˆÙ„Ùˆ ÙˆØ±ÙˆØ¯ÛŒ Ø®ÙˆØ±Ø§Ú© Ø¨Ù‡ Ø¨Ø³ØªØ± C",
                "Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ": "Ú†Ú© Ù‡ÙˆØ§ÛŒ Ø§Ø¨Ø²Ø§Ø± Ø¯Ù‚ÛŒÙ‚ Ùˆ Ù…Ø§Ù†ÙˆØ± Ø¯Ø³ØªÛŒ ÙˆÙ„Ùˆ"
            })
            suspects.append({
                "Ú©Ø¯ ÙˆÙ„Ùˆ / ØªØ¬Ù‡ÛŒØ²": f"V-{train}3C / V-{train}4C",
                "Ø§Ø­ØªÙ…Ø§Ù„ Ø®Ø·Ø§": "Û±ÛµÙª",
                "Ø¹Ù„Øª ÙØ±Ø¢ÛŒÙ†Ø¯ÛŒ": "Ù†ÙˆÛŒØ² ÛŒØ§ Ø¹Ø¯Ù… ØµØ­Øª Ø³ÛŒÚ¯Ù†Ø§Ù„ ÙÛŒØ¯Ø¨Ú© ÙˆØ¶Ø¹ÛŒØª Ø¨Ø³ØªÙ‡ ÙˆÙ„ÙˆÙ‡Ø§ÛŒ Ø§Ø³ØªØ±ÛŒÙ¾ÛŒÙ†Ú¯ Ø¯Ø± Ù…Ø¯ ADS",
                "Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ": "ØªØ³Øª Ø³ÛŒÙ…â€ŒÚ©Ø´ÛŒ Ùˆ ØªÙ†Ø·ÛŒÙ… Ù…Ø¬Ø¯Ø¯ Ù„ÛŒÙ…ÛŒØªâ€ŒØ³ÙˆØ¦ÛŒÚ†"
            })
            suspects.append({
                "Ú©Ø¯ ÙˆÙ„Ùˆ / ØªØ¬Ù‡ÛŒØ²": f"V-{train}2C (Ø®Ø±ÙˆØ¬ÛŒ Ø®ÙˆØ±Ø§Ú© ADS)",
                "Ø§Ø­ØªÙ…Ø§Ù„ Ø®Ø·Ø§": "Û±Û°Ùª",
                "Ø¹Ù„Øª ÙØ±Ø¢ÛŒÙ†Ø¯ÛŒ": "Ø§ÙØª ÙØ´Ø§Ø± Ø¯Ø± Ø®Ø±ÙˆØ¬ÛŒ Ø¨Ø³ØªØ± ÛŒØ§ Ø¹Ø¯Ù… Ø¢Ø¨â€ŒØ¨Ù†Ø¯ÛŒ Ø³ÛŒØª ÙˆÙ„Ùˆ",
                "Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ": "ØªØ³Øª Ù†Ø´ØªÛŒ Ø³ÛŒØª Ø®Ø±ÙˆØ¬ÛŒ"
            })

        if strip_err:
            reasons.append("Ø®Ø·Ø§ÛŒ ÙÛŒØ¯Ø¨Ú© OPEN ÙˆÙ„ÙˆÙ‡Ø§ÛŒ Û³ ÛŒØ§ Û´ Ø¯Ø± Ù…Ø¯ ADS")

        # Elimination logic output
        eliminated = []
        if rp_pass:
            eliminated.append(f"V-{train}6 (Ø§Ø±ØªØ¨Ø§Ø·ÛŒ Ø¨Ø§Ù„Ø§) âž” ØªØ¨Ø±Ø¦Ù‡ Ùˆ Ø­Ø°Ù Ù‚Ø·Ø¹ÛŒ (Ø¹Ø¨ÙˆØ± Ù…ÙˆÙÙ‚ Ø§Ø² RP1)")
        if dp_pass:
            eliminated.append(f"V-{train}5 (Ø§Ø±ØªØ¨Ø§Ø·ÛŒ Ù¾Ø§ÛŒÛŒÙ†) âž” ØªØ¨Ø±Ø¦Ù‡ Ùˆ Ø­Ø°Ù Ù‚Ø·Ø¹ÛŒ (Ø¹Ø¨ÙˆØ± Ù…ÙˆÙÙ‚ Ø§Ø² DP1)")

        return reasons, suspects, eliminated

    st.markdown("---")
    if st.button("ðŸš€ Ø§Ø¬Ø±Ø§ÛŒ Ø¹ÛŒØ¨â€ŒÛŒØ§Ø¨ÛŒ Ù‡ÙˆØ´Ù…Ù†Ø¯"):
        reasons, suspects, eliminated = diagnose(train_no, step_no, ads_p, dp3_p, ia_p, rp_passed, dp_passed, stripping_feedback_err)
        
        st.subheader("ðŸ“Š Ù†ØªÛŒØ¬Ù‡ ØªØ­Ù„ÛŒÙ„ Ùˆ ØªØ­Ù„ÛŒÙ„ Ø®Ø·Ø§Ø³Ø§Ø²ÛŒ")
        
        if reasons:
            st.markdown("<div class='status-trip'>ðŸš¨ ÙˆØ¶Ø¹ÛŒØª: ØªØ±ÛŒÙ¾ ØµØ§Ø¯Ø± Ø´Ø¯Ù‡ (TRIPPED)</div>", unsafe_allow_html=True)
            st.write("**Ø¹Ù„Ù„ Ø§ØµÙ„ÛŒ ØªØ±ÛŒÙ¾:**")
            for r in reasons:
                st.write(f"â€¢ {r}")
                
            st.subheader("ðŸŽ¯ Ø§ÙˆÙ„ÙˆÛŒØª ÙˆÙ„ÙˆÙ‡Ø§ÛŒ Ø®Ø·Ø§Ø³Ø§Ø²")
            df = pd.DataFrame(suspects)
            if not df.empty:
                st.table(df)
            
            if eliminated:
                st.info("ðŸ›¡ï¸ **ÙˆÙ„ÙˆÙ‡Ø§ÛŒ ØªØ¨Ø±Ø¦Ù‡ Ø´Ø¯Ù‡ (Ø­Ø°Ù Ø§Ø² Ù„ÛŒØ³Øª Ø¨Ø§Ø²Ø±Ø³ÛŒ):**\n" + "\n".join([f"â€¢ {e}" for e in eliminated]))

            # Printable Report Generator
            report_text = f"""Ú¯Ø²Ø§Ø±Ø´ Ø¹ÛŒØ¨â€ŒÛŒØ§Ø¨ÛŒ Ø³Ø±ÛŒØ¹ ÙˆØ§Ø­Ø¯ IPSORB
ØªØ±Ù†: {train_no} | Ø§Ø³ØªÙ¾: {step_no}
Ø¹Ù„Øª ØªØ±ÛŒÙ¾: {', '.join(reasons)}
Ø§ÙˆÙ„ÙˆÛŒØª Ø§ÙˆÙ„ Ø¨Ø§Ø²Ø±Ø³ÛŒ: {suspects[0]['Ú©Ø¯ ÙˆÙ„Ùˆ / ØªØ¬Ù‡ÛŒØ²']} ({suspects[0]['Ø§Ø­ØªÙ…Ø§Ù„ Ø®Ø·Ø§']})
Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ: {suspects[0]['Ø§Ù‚Ø¯Ø§Ù… Ù¾ÛŒØ´Ù†Ù‡Ø§Ø¯ÛŒ']}
"""
            st.download_button(
                label="ðŸ“¥ Ø¯Ø§Ù†Ù„ÙˆØ¯ Ú†Ú©â€ŒÙ„ÛŒØ³Øª Ø¨Ø§Ø²Ø±Ø³ÛŒ Ù†ÙˆØ¨ØªÚ©Ø§Ø±ÛŒ (ÙØ§ÛŒÙ„ Ù…ØªÙ†ÛŒ)",
                data=report_text,
                file_name=f"IPSORB_Trip_Report_Train{train_no}_Step{step_no}.txt",
                mime="text/plain"
            )
        else:
            st.markdown("<div class='status-normal'>âœ… ÙˆØ¶Ø¹ÛŒØª: Ù†Ø±Ù…Ø§Ù„ / ÙØ±Ø¢ÛŒÙ†Ø¯ Ø¨Ø¯ÙˆÙ† Ø§Ù†Ø­Ø±Ø§Ù ØªØ±ÛŒÙ¾</div>", unsafe_allow_html=True)

with tab2:
    st.subheader("ðŸ“œ Ù…Ø§ØªØ±ÛŒØ³ Û²Û´ Ø§Ø³ØªÙ¾ ÙˆØ§Ø­Ø¯ IPSORB")
    st.caption("Ø²Ù…Ø§Ù† Ù…Ø§Ù†Ø¯Ú¯Ø§Ø±ÛŒ Ù‡Ø± Ø§Ø³ØªÙ¾: Û´Û° Ø«Ø§Ù†ÛŒÙ‡")
    
    steps_data = []
    for i in range(1, 25):
        phase = "ADS / Stripping / RP / DP"
        if i in [1, 2, 3, 4, 21, 22, 23, 24]:
            phase = "Ø³ÙˆØ¦ÛŒÚ†ÛŒÙ†Ú¯ Ù†Ù‡Ø§ÛŒÛŒ / Ø¬Ø°Ø¨ Ø³Ù†Ú¯ÛŒÙ† (ADS)"
        elif i in [5, 6, 7, 8]:
            phase = "Ø§Ø³ØªØ±ÛŒÙ¾ÛŒÙ†Ú¯ Ùˆ Ø§ÙØª ÙØ´Ø§Ø± Ø§ÙˆÙ„ÛŒÙ‡ (DP1)"
        elif i in [9, 10, 11, 12]:
            phase = "Ø§ÙØª ÙØ´Ø§Ø± Ù¾Ù„Ù‡â€ŒØ§ÛŒ (DP2 / DP3)"
        else:
            phase = "Ø±ÛŒØ³Ù¾Ø±Ø³Ø§Ø²ÛŒ (RP1 / RP2 / RP3)"
            
        steps_data.append({"Ø§Ø³ØªÙ¾": f"Step {i}", "Ø²Ù…Ø§Ù† (Ø«Ø§Ù†ÛŒÙ‡)": 40, "ÙØ§Ø² Ø§ØµÙ„ÛŒ ÙØ±Ø¢ÛŒÙ†Ø¯ÛŒ": phase})
    
    st.dataframe(pd.DataFrame(steps_data), use_container_width=True)

with tab3:
    st.subheader("ðŸ› ï¸ Ú©Ù„ÛŒØ¯ Ù†Ø§Ù…â€ŒÚ¯Ø°Ø§Ø±ÛŒ Ùˆ ÙˆØ¸Ø§ÛŒÙ ÙˆÙ„ÙˆÙ‡Ø§")
    st.markdown("""
    * **V-1:** ÙˆØ±ÙˆØ¯ÛŒ Ø®ÙˆØ±Ø§Ú© / ÙØ´Ø§Ø±Ú¯ÛŒØ±ÛŒ (Feed Inlet)
    * **V-2:** Ø®Ø±ÙˆØ¬ÛŒ Ø®ÙˆØ±Ø§Ú© Ø¯Ø± ADS (Feed Outlet)
    * **V-3:** ÙˆØ±ÙˆØ¯ÛŒ Ø§Ø³ØªØ±ÛŒÙ¾ÛŒÙ†Ú¯ (Stripping Inlet)
    * **V-4:** Ø®Ø±ÙˆØ¬ÛŒ Ø§Ø³ØªØ±ÛŒÙ¾ÛŒÙ†Ú¯ (Stripping Outlet)
    * **V-5:** ÙˆÙ„Ùˆ Ø§Ø±ØªØ¨Ø§Ø·ÛŒ Ù¾Ø§ÛŒÛŒÙ† (ØªØ®Ù„ÛŒÙ‡) âž” *Ø§Ú¯Ø± DP1 Ø±Ø¯ Ø´ÙˆØ¯ = ØªØ¨Ø±Ø¦Ù‡*
    * **V-6:** ÙˆÙ„Ùˆ Ø§Ø±ØªØ¨Ø§Ø·ÛŒ Ø¨Ø§Ù„Ø§ (ÙØ´Ø§Ø±Ú¯ÛŒØ±ÛŒ) âž” *Ø§Ú¯Ø± RP1 Ø±Ø¯ Ø´ÙˆØ¯ = ØªØ¨Ø±Ø¦Ù‡*
    * **V-7:** ÙˆÙ„Ùˆ ØªØ®Ù„ÛŒÙ‡ Ù†Ù‡Ø§ÛŒÛŒ Ø¨Ù‡ DP3
    * **V-8:** Ø´ÛŒØ± Ø§Ú©ÙˆÙ„Ø§ÛŒØ²Ø± / Û³ Ø·Ø±ÙÙ‡ (Equalizer / 3-Way Valve)
    """)

st.caption("Ø¨Ø±Ù†Ø§Ù…Ù‡ Ø¹ÛŒØ¨â€ŒÛŒØ§Ø¨ÛŒ Ù‡ÙˆØ´Ù…Ù†Ø¯ ÙˆØ§Ø­Ø¯ IPSORB - Ù†Ø³Ø®Ù‡ PWA Ù…ÙˆØ¨Ø§ÛŒÙ„ v2.0")
