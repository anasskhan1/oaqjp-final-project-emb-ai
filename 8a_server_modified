"""Flask server for the emotion detection application."""

from flask import Flask, render_template, request
from EmotionDetection.emotion_detection import emotion_detector

app = Flask(__name__)


@app.route("/")
def render_index_page():
    """Render the main application page."""
    return render_template("index.html")


@app.route("/emotionDetector")
def emotionDetector():  # pylint: disable=invalid-name
    """Analyze the text provided by the user."""
    text_to_analyze = request.args.get("textToAnalyze")

    response = emotion_detector(text_to_analyze)

    if isinstance(response, tuple):
        response, status_code = response
    else:
        status_code = 200

    if response.get("dominant_emotion") is None:
        return "Invalid text! Please try again!", status_code

    anger = response["anger"]
    disgust = response["disgust"]
    fear = response["fear"]
    joy = response["joy"]
    sadness = response["sadness"]
    dominant_emotion = response["dominant_emotion"]

    return (
        "For the given statement, the system response is "
        f"anger: {anger}, "
        f"disgust: {disgust}, "
        f"fear: {fear}, "
        f"joy: {joy}, "
        f"sadness: {sadness}. "
        f"The dominant emotion is {dominant_emotion}."
    )


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
