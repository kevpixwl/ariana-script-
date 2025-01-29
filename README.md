local function removePartsWithTouchInterest()
    for _, part in ipairs(workspace:GetDescendants()) do
        if part:IsA("BasePart") and part:FindFirstChild("TouchInterest") then
            part:Destroy()
        end
    end
end
removePartsWithTouchInterest()
-- script for ariana --
