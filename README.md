# .github-workflows-test.yml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.9"

      - name: Install dependencies
        run: |
          python -m venv venv
          source venv/bin/activate
          pip install -r requirements.txt

      - name: Run pylint
        run: |
          source venv/bin/activate
          pylint calculator/

      - name: Run pytest
        run: |
          source venv/bin/activate
          pytest --cov=calculator
