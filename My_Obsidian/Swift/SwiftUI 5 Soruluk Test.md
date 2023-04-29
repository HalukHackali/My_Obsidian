#yazılım #swift 

```swift
import SwiftUI

struct Question {
    let text: String
    let answers: [String]
    let correctAnswer: Int
}

struct QuizView: View {
    let questions = [
        Question(text: "What is the capital of France?", answers: ["Berlin", "Paris", "London", "Madrid"], correctAnswer: 1),
        Question(text: "What is the highest mountain in the world?", answers: ["Everest", "K2", "Kilimanjaro", "Denali"], correctAnswer: 0),
        Question(text: "Who is the author of 'To Kill a Mockingbird'?", answers: ["Harper Lee", "John Steinbeck", "F. Scott Fitzgerald", "Ernest Hemingway"], correctAnswer: 0),
        Question(text: "What is the largest animal in the world?", answers: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"], correctAnswer: 1),
        Question(text: "What is the currency of Japan?", answers: ["Yuan", "Euro", "Dollar", "Yen"], correctAnswer: 3)
    ]
    
    @State private var currentQuestionIndex = 0
    @State private var selectedAnswerIndex: Int? = nil
    @State private var score = 0
    
    var body: some View {
        VStack(alignment: .leading, spacing: 20) {
            Text("Question \(currentQuestionIndex + 1): \(questions[currentQuestionIndex].text)")
                .font(.title)
            ForEach(0..<4) { index in
                Button(action: {
                    selectedAnswerIndex = index
                    checkAnswer()
                }, label: {
                    Text("\(questions[currentQuestionIndex].answers[index])")
                        .foregroundColor(.white)
                        .padding()
                        .background(selectedAnswerIndex == index ? Color.blue : Color.gray)
                        .cornerRadius(10)
                })
            }
            Spacer()
        }
        .padding()
    }
    
    func checkAnswer() {
        if let selectedAnswerIndex = selectedAnswerIndex {
            if selectedAnswerIndex == questions[currentQuestionIndex].correctAnswer {
                score += 1
            }
            if currentQuestionIndex == questions.count - 1 {
                // End of quiz
                showResult()
            } else {
                // Move to next question
                currentQuestionIndex += 1
                selectedAnswerIndex = nil
            }
        }
    }
    
    func showResult() {
        let message = "You scored \(score) out of \(questions.count)."
        let alert = UIAlertController(title: "Quiz Result", message: message, preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: "OK", style: .default, handler: { action in
            // Reset quiz
            currentQuestionIndex = 0
            selectedAnswerIndex = nil
            score = 0
        }))
        UIApplication.shared.windows.first?.rootViewController?.present(alert, animated: true)
    }
}

struct QuizView_Previews: PreviewProvider {
    static var previews: some View {
        QuizView()
    }
}
```