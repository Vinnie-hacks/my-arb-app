import streamlit as st

# App Setup
st.set_page_config(page_title="Genius Arb 2025", page_icon="📈")
st.title("🇰🇪 Genius Arbitrage Calculator")
st.markdown("---")

# Input Section in Sidebar
st.sidebar.header("Match Parameters")
capital = st.sidebar.number_input("Total Capital (KES)", value=15000, step=500)
mode = st.sidebar.radio("Select Strategy", ["Accumulation (Profit)", "Migration (Shift Funds)"])

col1, col2 = st.columns(2)
with col1:
    odds_safe = st.number_input("1xBet Odds (Favorite)", value=1.20)
with col2:
    odds_taxed = st.number_input("Taxed Bookie Odds", value=7.50)

# The Math Logic
tax = 0.05
if st.button("Calculate Stakes"):
    if mode == "Accumulation (Profit)":
        # Standard Profit Bias
        stake_taxed = (capital * (1 + tax)) / odds_taxed
        stake_safe = capital - stake_taxed
    else:
        # Migration Bias (Empty the taxed tank)
        stake_taxed = capital / (odds_taxed * (1 - tax))
        stake_safe = capital - stake_taxed

    # Rounding for "Human" look
    r_safe = round(stake_safe / 50) * 50
    r_taxed = round(stake_taxed / 50) * 50

    # Display Results
    st.markdown("### 🎯 Your Betting Plan")
    st.info(f"**BET THIS on 1xBet:** {r_safe:,} KES")
    st.warning(f"**BET THIS on Taxed Bookie:** {r_taxed:,} KES")
    
    # Profit Projections
    p_safe = (r_safe * odds_safe) - (r_safe + r_taxed)
    p_taxed = (r_taxed * odds_taxed * (1-tax)) - (r_safe + r_taxed)
    
    st.write(f"Profit if 1xBet wins: **{round(p_safe, 2)} KES**")
    st.write(f"Profit if Taxed wins: **{round(p_taxed, 2)} KES**")
