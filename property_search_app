import streamlit as st
import requests

# API Configuration
API_BASE_URL = "https://use-land-property-data.service.gov.uk/api/v1/"
API_KEY = "ff9ddc5b-b510-4562-99df-f65e9ea0846d"

headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Accept": "application/json"
}

# Streamlit Web Interface
st.title("🔍 UK Land & Property Data Search")

proprietor_name = st.text_input("Enter Proprietor Name:")

if st.button("Search Properties"):
    if proprietor_name:
        with st.spinner("Searching properties..."):
            response = requests.get(
                f"{API_BASE_URL}properties",
                headers=headers,
                params={"proprietor_name": proprietor_name}
            )

            if response.status_code == 200:
                data = response.json()
                results = data.get("results", [])
                if results:
                    st.success(f"Found {len(results)} properties!")
                    for prop in results:
                        st.subheader(f"{prop.get('address', 'N/A')}")
                        st.write(f"- **Postcode:** {prop.get('postcode', 'N/A')}")
                        st.write(f"- **Title Number:** {prop.get('title_number', 'N/A')}")
                        st.write(f"- **Tenure:** {prop.get('tenure', 'N/A')}")
                        st.write(f"- **Last Sale Date:** {prop.get('last_sale_date', 'N/A')}")
                        st.write(f"- **Last Sale Price:** {prop.get('last_sale_price', 'N/A')}")
                        st.markdown("---")
                else:
                    st.warning("No properties found for this proprietor.")
            else:
                st.error(f"API Error: {response.status_code}")
    else:
        st.warning("Please enter a proprietor name.")
