name: CAT_A_01


on:
  
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  
  workflow_dispatch:
env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}


jobs:
  
  build:
    
    runs-on: self-hosted


    
    steps:
      
      - name: Generate build number
        id: buildnumber
        uses: einaregilsson/build-number@v3
        with:
            token: ${{secrets.github_token}}  
      - uses: actions/checkout@v2

        
      - name: Create Jars Folder
        run: mkdir bars
        
      - name: Build RBS_AccountBalanceDetails_v1 Project
        run: |
            cd RBS_AccountBalanceDetails_v1
            ant -noinput -buildfile build.xml
            mv /root/*.bar ../bars/RBS_AccountBalanceDetails_v1_${{ steps.buildnumber.outputs.build_number }}.bar
      - name: Build RBS_FXRateInquiry_v3 Project
        run: |
            cd RBS_FXRateInquiry_v3
            ant -noinput -buildfile build.xml
            mv /root/*.bar ../bars/RBS_FXRateInquiry_v3_${{ steps.buildnumber.outputs.build_number }}.bar
      - name: Build RBS_EnquireBeneficiaryDetails_v1 Project
        run: |
            cd RBS_EnquireBeneficiaryDetails_v1
            ant -noinput -buildfile build.xml
            mv /root/*.bar ../bars/RBS_EnquireBeneficiaryDetails_v1_${{ steps.buildnumber.outputs.build_number }}.bar
      - name: Build RBS_FetchBeneficiaryBanksList_v1 Project
        run: |
            cd RBS_FetchBeneficiaryBanksList_v1
            ant -noinput -buildfile build.xml
            mv /root/*.bar ../bars/RBS_FetchBeneficiaryBanksList_v1_${{ steps.buildnumber.outputs.build_number }}.bar
      - name: Build RBS_FetchFXDealList_v1 Project
        run: |
            cd RBS_FetchFXDealList_v1
            ant -noinput -buildfile build.xml
            mv /root/*.bar ../bars/RBS_FetchFXDealList_v1_${{ steps.buildnumber.outputs.build_number }}.bar
      - name: Build RBS_LoanAccountDetails_v2 Project
        run: |
            cd RBS_LoanAccountDetails_v2
            ant -noinput -buildfile build.xml
            mv /root/*.bar ../bars/RBS_LoanAccountDetails_v2_${{ steps.buildnumber.outputs.build_number }}.bar
  
      # Runs a set of commands using the runners shell
      - name: Check jars folder
        run: |
          cd bars
          ls
