require "csv"

def classify_signal(score)
  if score >= 34
    "HIGH SIGNAL"
  elsif score >= 28
    "STRONG"
  elsif score >= 20
    "MODERATE"
  else
    "LOW PRIORITY"
  end
end

def calculate_score(record)
  record["alignment"].to_i +
    record["leverage"].to_i +
    record["credibility"].to_i +
    record["ease"].to_i
end

def parse_records(filename)
  records = []

  CSV.foreach(filename, headers: true) do |row|
    score = calculate_score(row)
    status = classify_signal(score)

    records << {
      name: row["name"],
      category: row["category"],
      score: score,
      status: status
    }
  end

  records.sort_by { |item| -item[:score] }
end

def print_ranked_summary(records)
  puts "Ranked Synthetic Signals"
  puts

  records.each_with_index do |item, index|
    puts "#{index + 1}. #{item[:name]} | #{item[:category]} | Score: #{item[:score]} | Status: #{item[:status]}"
  end
end

records = parse_records("sample_records.csv")
print_ranked_summary(records)
